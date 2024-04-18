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

### The Accidental DBA by Clay Jackson

* 
