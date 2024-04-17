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
  * Anecdotally, I heard from another conference attendee that dbeaver is super helpful for them in observability
 
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

### Zero-downtime Postgres Major Version Upgrades by Biren Shah

Biren is a Senior Database Reliability Engineer at GitLab


#### Zero downtime

* The presenter called zero downtime a "clickbait title" 🤣.
* Zero downtime means all services are available to end users.  No request is instantaneous, so they determine "Apdex", the threshold of how it is still usable.

#### Postgres upgrades: how do they work and why are they hard?

* Minor version upgrades -- mainly you can just put the new binary in place and restart
* Major version upgrades are much more complex

#### Upgrade methods

* pg_dumpall: this has the most downtime, and can be resource intensive.  It is the safest method available, so if it meets your needs, just do it!
* pg_upgrade: simple, reasonably fast and safe, but there is no rollback if something goes wrong.  Still has downtime.  But if it's within your threshold, no need to do something more complex

#### Gitlab infrastructure

* Primary and secondary, using patroni for streaming replication
* Rails connects to PgBouncer
* Uses Consul to handle the replicas

#### How they used to do it

1. Create second cluster from a disk snapshot (they don't do a logical replication from scratch, since it will take forever!)
2. Sync new with main cluster
3. Put gitlab into maintenance (read-only) mode for several hours
4. pg_upgrade primary
5. Recreate standby
6. Run QA tests and benchmark (this is the most time-consuming part, but it is important since there is no rollback)

Bad impact on users, and they really avoided major upgrades as a result.

#### How do they do it now

The answer is: logical replication and [some really cool ansible playbooks](https://gitlab.com/gitlab-com/gl-infra/db-migration)

Issues with logical
* Some schema changes are not replicated.  To resolve this: they have a feature flag to stop all DDL changes.  When the feature flag is off, it queues those changes.  When they turn the feature flag back on, any DDL changes that were queued. 
* Sequences are not replicated, so SERIAL/AUTO INCREMENT will break.  To resolve this: measure the daily growth of all sequences.  They found that if they just increase the sequence by 1 million during the migration, they won't run into the issue.
* Each table needs a replica identity (e.g. primary key).  They already had this, so no problem.
* It is more complex (prone to human errors, so big need for automation and testing).  They ansible-ized it, and it works great.  They also do tons of testing: "If it hurts, do it more often".  They ran several dry runs in production in advance.

As part of their process, they run both $SOURCE and $TARGET in tandem, with half of all requests going to the new, and half going to the old.  Ansible does a lot of automated checks to make sure that $TARGET is working well, including checking for long-running transactions, autovacuum issues

The application is also smart: it can tell how fresh a replica is, and if it is not fresh enough, choose a different one.  Also, if it needs a read-only or a read-write node.

The playbook checks for zombie processes, long-running things, and it just stops execution if they are not in a good state.

pgBouncer: they run PAUSE, which will finish all the existing connections.  Wait until the logical replication lag is zero bytes, then they run RESUME on pgBouncer.  Their ansible playbook will be running consistently to check the amount of logical replication lag, and then they use that to find a low-traffic time.

They compared the apdex of the upgrade to the normal range of apdex.  There is a measurable change in apdex during the switchover.  But it is still well within their threshold, and was not even the lowest apdex they would have during that date.

[More about their database infrastructure](https://handbook.gitlab.com/handbook/engineering/infrastructure/database/).

### Schema Evolution - The Hard Parts by Gwen Shapira
