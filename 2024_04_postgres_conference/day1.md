### Synergy: Teamwork makes the dream work by Zak Tedder

* Realistic Conflict Theory
  * Tension will arrive when competing for limited resources (in an organization, it's not just about funding, the resources could be respect, power, or recognition)

### Why we put GPUs in the database by Montana Low

* Talked about instacart
   * Instacart was experimenting with migrating from ElasticSearch to Postgres for scaling issues
   * Then the pandemic happened, and they had a huge outage during a busy grocery shopping day
   * To relieve the pressure, they switched to the relatively untested postgres cluster.  It quickly started timing out too, but `pg_stat_statements` showed them an easy fix: just add an index.  They were able to get things working.
   * They use [PgCat](https://www.instacart.com/company/how-its-made/adopting-pgcat-a-nextgen-postgres-proxy/), rather than PgBouncer
* Talked about the new machine learning project, [PostgresML](https://github.com/postgresml/postgresml) -- it's a database extension in your local database, so you don't have to wait for network latency for talking to, say, ChatGPT API

### Managing at scale Postgres version upgrades with minimum downtime by Jignesh Shah

* Major version upgrades take a lot of planning and work
* There are many types of database changes:
  * minor/major upgrades
  * security/bugfix updates
  * OS updates
  * scaling
  * engine parameter changes
  * schema changes
  * A database upgrade could involve all of the above!
* Two main strategies
  * In-place (e.g. with pg_upgrade).  Simple, but downtime of an unpredictable duration
  * Blue/green, where you upgrade staging, then switch over.
    * RDS Blue/Green deployments is their implementation
    * First, set up logical replication from blue to green.
    * Make the change in green.  Test (and confirm that logical replication is still working and getting you the updates)
    * Promote green
      * Configuration timeout for current database connections, long-running transactions
    * This is safe and fast.  AWS's automation makes it easy for the user.
    * Logical replication needs to be enabled
      *  Limitations:
        *  DDL is not replicated.  So you can't make schema changes during this period in blue, since they will not appear in green
        *  You need primary keys
        *  Large objects (not to be confused with BLOB, BYTEA, TEXT) are not replicated
* How Amazon RDS does it:
  * Before proceeding, upgrade extensions like PostGIS.
  * First, create a point-in-time replica (PITR), then upgrade, then create a new PITR.  If things don't work out right, roll back to the first and there will not be data loss.
    * The replica can take a really long time
    * Run VACUUM ANALYZE after the in-place upgrade, since pg_upgrade doesn't do this
  * Always upgrade to the most recent version (e.g. if you are on postgres 11, just jump to 16.  Don't jump to 12, because it will go EOL right away)
* Recommendation:
  * Upgrade dev environments in place
  * Upgrade pre-prod environments with blue/green, so you can see what issues come up
  * Upgrade prod environments with blue/green


### Looking for differences in your data by Tatiana Krupenya

Very good talk!

#### When do we need to compare data?
* Stage-prod synchronization
* DB migration
* Finding the delta in backups

#### What are we looking for?
* Added rows
* Deleted rows
* Modified rows

#### How to compare?

* First instinct is to just check with your eyes.  But this does not scale to complex data types, lots of data
* Next instinct is to export and look at in Excel.  But the challenges are that you need to export the data, get it to a computer with Excel, think of good Excel magic
* Okay, maybe we can do some joins (`select lt* where not exists (select from rt)`).  Limitation is that the tables need to be in the same database, and even worse, these queries can be very memory-intensive.
* Using an application like [dbeaver](https://github.com/dbeaver/dbeaver).  Its enterprise version has a data compare feature, which works like:
  * Just grab `SELECT *` from both tables, no memory consumption issues from a join
  * Then identify IDs that only in exist in one or the other.
  * Then look at IDs that are in both, and see if they are the same.
  * At the end, it gives you the SQL you would need to make the two tables the same
  * Disadvantages: you need a third-party app (and the open source version of dbeaver doesn't have it), composite keys make it more challenging, and requires disk space
 
All of the above work in certain circumstances.

### Troubleshoot PostgreSQL performance by use case by Wanda He and Thuymy Tran

#### Postgres architecture

* Processes
  * postmaster is the primary process
  * each connection has a relevant backend process (a worker process) which communicates with the client connection -- a client connection never has direct access to memory
  * utility processes: autovacuum, checkpointer, etc.
* Memory
  * Global shared memory
    * Shared buffers
    * WAL buffers
  * Local private memory
    * Per-process memory
    * Caches for metadata, execution plan, query execution memory
* Storage
    * Data files (the base subdirectory)
    * WAL files (the pg_wal subdirectory)

#### Key performance factors

* CPU
  * Sub-optimal query
  * Too many active connections
  * Is `max_parallel_workers_per_gather` too high?
  * Monitor: % total cpu, % system cpu, % wait cpu
* Memory
  * High # of connections
  * Sub-optimal memory intensive query
  * Have you done some bad configuration (e.g. did you set `work_mem` high -- it is per connection and per SORT!)
  * Monitoring: `pg_proctab` extension, `pg_backend_memory_contexts`,  `pg_log_backend_memory_contexts`, freeable memory, % buffer cache hit ratio
* Storage
  * Not enough space
  * Table/index bloat means that vacuuming is not effective, so it has to consult a lot of pages for each query
  * Checkpoints need tuning
  * IOPs, MB/s, disk read/write latency per IO
* the patterns you use in your application to access the db
  * Blocking / locking
  * Long-running transactions
  * Idle in transaction
  * Idle connections


#### Specific use cases

* Idle connections
  * Misconception that they do not affect performance.
  * They did a demo with 1,000 idle connections, and we saw that freeable memory went way down
  * Recommendation: use a connection pooler.  They used RDS proxy endpoint.  You could use pgbouncer.
  * They did the same demo with 1,000 connections, and the memory didn't drop!  And only the needed 12 connections actually used memory on the postgres.
  * You can add up a lot, if lots of applications are each opening, say, 10 connections
* VACUUM is being blocked (perhaps by a long-running transaction that is using that tuple, so it can't be cleaned up)
  * Demo: set up a long-running transaction
  * Look at running time and buffers, running time went up and up.
  * logical replication can also affect autovacuum
  * They did a query to find what process was blocking, and what it was doing.  Then they terminated the transaction.
  * There is also an idle_in_transaction_timeout setting in postgres.  But it's more important to check your application code to make sure you are closing transactions properly

#### Tips for better performance

1. Use pgbouncer to handle lots of connections
1. Make sure vacuuming is working well.  Monitor vacuuming to make sure that it is containing bloat.
1. Tune query performance
1. Avoid long-running transactions, avoid a storm of connections, avoid subtransactions, and don't use FKs excessively
