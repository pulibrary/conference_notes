### I implemented the first vacuum cleaner daemon by Curt Kolovson

* Original design of postgres storage system (1987) was to keep all past states of tuples in an immutable way.
  * This way you could time travel, rollback to an old state
  * The idea was that you could vacuum historical data to archive storage (WORM drives)
  * But this was deprecated
* The speaker implemented the early version of the vacuum cleaner daemon (the code is long gone by now, and it was all about moving old data to storage, rather than removing obsolete tuples) 
* What can we learn from this today?
  * Bitemporal data model: effective time (when a tuple is active) and asserted time (when a tuple exists in the database, whether active or not.  You can assert a time in the future).
    * Primary keys are actually a combination of the key, effective time and asserted time
    * Use cases: security and auditing (permissions/RBAC), anywhere you need to time travel forward or back, or view a changelog of a tuple, disaster recovery (point-in-time recovery)
    * Any data from the past must be immutable
  * Maybe it's time to bring this back, and make it actually happen in Postgres.  It is available in some major commercial dbs.

### MERGE() - a quick introduction by Dave Stokes

[Slides](https://postgresconf.org/system/events/document/000/002/130/PGNYC_Merge__1_.pdf)

* Several use cases
  * UPSERT using sort of case statements
  * DELETE if there is a match
  * DO NOTHING if there is a match
  * the WHEN can be "matched" or it can be a more complex condition
* It gets complicated when you also use database triggers
* New features coming in 17:
  * RETURNING merge_action(), which gives you a summary of what it did
* I can absolutely see us using this, it was added in postgres 15
* It is very performant on large tables


### Everything you want to know about Postgres autovacuum by Bohan Zhang

#### Multi-Version Concurrency Control (MVCC) in postgresql

* When you update an existing row, postgres makes a copy of the row and applies the changes to the new version, rather than overwriting.
  * This is so that read operations don't block write operations, and vice versa
* To know which is the most recent copy of the tuple, it uses an oldest-to-newest O2N version chain
  * Each outdated tuple also has a link to the version that superseded it
  * Postgres has to traverse this chain to figure out which tuple to use
  * During a table scan, you need to read all the outdated tuples into memory as well as all the current ones
  * Indexes can help postgres by recording this chain.  It helps with query performance, but it makes writes more expensive if you have a lot of versions of the tuple.
  * For very bloated tables, it can interfere with statistics, which can interfere with query planning (so you might get an inefficient plan)

#### Autovacuum in postgresql

* Autovacuum helps with table bloat
* VACUUM vs VACUUM FULL
  * VACUUM is much faster, but it does not return the disk space
  * VACUUM FULL will return disk space, but it is time-consuming and resource-intensive -- you should be very careful doing this in prod
* ANALYZE updates statistics used by the planner
  * The presenter gave an example where ANALYZE had never been run.  The planner thought there was only one row (so it used SeqScan), but it actually had 3 million rows!
* Autovacuum automates the execution of VACUUM and ANALYZE.
* For large tables, you should set the autovacuum_vacuum_scale_factor and analyze_factor lower.
  * Example of a table with 1 billion rows, it won't vacuum by default until you have 200 million dead tuples, which will have serious performance issues
* Long-running transactions can block autovacuum.  Monitor it!  With pg_stat_*.  Also with how many dead tuples there are.
* Don't trust `pg_stat_all_tables.last_autovacuum` - it is the last time it was run, even if it was blocked by a lock
* By default, there are 3 autovacuum workers. So even if your table is due for an autovacuum, the workers might be vacuuming something else.  You can also configure how much/likely the workers are to sleep between autovacuuming.

### Becoming a PG_STAT_* (star) by Chirag Dave and Sami Imseih

#### Dynamic views

* These have a PID (process id) column
* The entry disappears when the connection closes
* `pg_stat_activity` is a famous one
  * important columns: pid, xact_start, query_start, state_change (when did it go between Active, Idle, Idle in transaction)
* `pg_stat_progress_vacuum`
  * vacuum has 6 or 7 different phases, like "scanning heap" (reading through the heap to find dead tuples).  This is in the phase column


#### Cumulative stats

This is what we will focus on today.

They are only snapshots.  You should run these regularly and calculate the deltas as part of your monitoring.

* pg_stat_wal: look at wal_fpi column (WAL full-page index) and wal_buffers_full
* pg_stat_bgwriter: buffers_backend should be as close to 0 as possible, it means less work that needs to be done at query time
* `pg_stat_all_tables`: maximize n_tup_hot_update (dropping unused indexes can help with this).  Also check VACUUM/ANALYZE stats: n_dead_tup and n_mod_since_analyze.
  * If _n_dead_tup_ keeps growing, something is wrong with your autovacuum
* In postgres 16+, you can see when the last seq scan was, to see how effective your indexes are.  If you are seeing seq scans on large tables, you need to work on those indexes.
* pg_stat_statements Uses an extension
* pg_statio_all_tables and pg_statio_all_indexes (per relation)
* pg_stat_io: useful and added in 16.  Look at context, extends, and evictions columns.  Also, to get an accurate cache hit ratio `(hits/(reads+hits)::numeric / 100)`.

#### postgres internals

* Writing in general:
  1. Write it to the WAL log
  2. Update shared buffers
  3. Hit a checkpoint
  4. Write it to the disk
* Shared buffers
  * These are a bunch of 8k pages that are in memory
  * You want the most popular things in shared_buffers, so you can get it from memory instead of disk.
  * During a query, postgres will evict cold pages (the pages that aren't popular or currently in use) to free up the space it might need
  * Ring buffers: they prevent cache thrashing (without it, if you did `SELECT * FROM huge_table` it would evict all the pages from the shared buffers, whether they are popular or not)
* HOT updates - I didn't follow this part

### Advanced strategies for PostgreSQL Lock Management by Greg Dostatni 

#### lock manager

* aka lmgr
* MVCC is critical to how lock manager works
  *  MVCC guarantees that while you are in a transaction, you see the version of the database as of the start of the transaction; work that other transactions have done since the beginning of the transaction should not affect the work you are doing.  Row versioning is how it achieves consistency and isolation
  *  Optimistic locking
  *  MVCC Considerations: Bloat, transaction id wraparound (the transaction id is 4 bytes, if it overflows, then it doesn't know what transaction's work goes first)
 
 * Lock-related structures in memory:
   * table of LOCKs in shared memory
   * table of PROCLOCKs in shared memory
   * For each process, a LOCALLOCK structure that keeps track of its locks.  And a fastpath (I didn't follow what that is)

#### Types of locks in lock manager

* Regular locks - these lock db objects, the ones that we usually see
* SIReadLocks - for enforcing very strict FIFO
* Spinlocks - may or may not be used much anymore.
* LWLocks (lightweight locks) - internal postgres processes trying to access shared memory or other resources

#### Questions that monitoring should answer

1. Which transaction is blocked
2. Which transaction is doing the blocking
3. Which objects get blocked the most
4. Average amount of time that things are blocked

### Monitoring PostgreSQL: Navigating the Landscape of Metrics, OS and Hardware Relationships, and Toolsets by Charly Batista

#### Goals of monitoring

* service availability
* performance optimization
* alerting and incident response
* capacity planning
* continuous improvement

#### metrics

CPU
* CPU utilization
* User vs System CPU time
* context switching -- recommended to check this, it's not something people think about as often

Memory Metrics
* Memory buffers and caches
* Page faults

Disk I/O
* I/O wait time

Network
* packet loss
* retries/retransmissions

postgres metrics
* full table scans
* checkpoint activity
* autovacuum activity
* long-running queries
* wait events from pg_wait_events (pg 17) -- will be very helpful.  It tells you _why_ something is waiting

procfs system

linux monitoring tools: sysstat package and 0x.tools

#### postgres monitoring tools

* Built-in
  * pg_stat_statements (or pg_stat_monitor, which is built on it and adds some features)
  * pg_buffercache
* External CLI
  * pg_view
  * pg_activity
* External web interfaces -- these expose metrics, but don't provide everything you need for monitoring
  * pgwatch2 and pgobserver

### PostgreSQL architecture considerations for application developers by Peter Celentano and Tracy Jenkins

### Miscellaneous

* [pg_search](https://blog.paradedb.com/pages/introducing_search) (part of ParadeDB) seems like an interesting project.  It tries to make postgres full-text search more like elasticsearch or solr.
