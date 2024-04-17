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
  * Disadvantages: you need a third-party app (and the open source version doesn't have it), composite keys make it more challenging, and requires disk space
 
All of the above work in certain circumstances.

### Troubleshoot PostgreSQL performance by use case by Wanda He and Thuymy Tran

