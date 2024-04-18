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


