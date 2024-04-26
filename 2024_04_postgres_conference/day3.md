### Transaction Isolation in Postgres by Gwen Shapira

This is based on [this blog post](https://www.thenile.dev/blog/transaction-isolation-postgres), which unfortunately doesn't use cat-related examples

* Example: feeding your cat!  In the same transaction, you note that you gave the cat some food, and that your cat food supply decreased
* Isolation is the "I" in ACID
* ANSI SQL92 definition of Isolation: when you have concurrent transactions, the result has to be the same as if you serialized those transactions: ran them sequentially instead of concurrently
  * At that time, they considered this impossible to achieve with reasonable performance.  So they made a list of possible anomalies, so you can understand the tradeoffs
 
#### Dirty read

* Dirty reads
  * Postgres does not have this.  Non-relational databases have this.
* Cat example:
  1. you buy cat food
  2. Open a transaction
  3. Add the food to the inventory
  5. Accidentally leave the cat food in the cafe!
  6. Partner checks the inventory, and sees some food that doesn't actually have it
  7. Rollback the transaction
 
#### Read committed

Default isolation level of postgres

* The issue is non-repeatable reads and write-after-read problem
* Cat example of non-repeatable read
  1. partner opens a transaction
  2. partner does a select to find how much the cat weighs
  3. you open a transaction and feed the cat and commit
  4. partner does another select within the same transaction as they used before.  The result is different!
* Cat example of write-after-read
  1. cat asks for food
  1. open a transaction
  2. check if the cat has eaten - no
  3. cat also asks partner for food
  4. partner opens a transaction and checks if cat has eaten - no
  5. you feed the cat, record it, and commit
  6. partner does the same, and the cat gets fed twice!

  Solutions to write-after-read:
  * include the criteria in the same update query
  * queues


#### Phantom reads

This comes from repeatable reads isolation level in the SQL 92 standard.  This came from before MVCC.  It's not clear that anyone still needs this.

* Microsoft research, 1995 - They found a bunch of new anomolies that could still happen even if transactions were serialized!
  * These weren't covered by the 92 standards
  * Postgres 9.2 introduced serializable snapshot isolation, which prevents all of the new anomolies
    * This also prevents phantom reads

#### Snapshots

* `SELECT * FROM pg_snapshot`
  * This contains the lowest XID such that you know that anything under it is uncommited

#### Isolation levels

* You can choose [transaction isolation levels](https://www.postgresql.org/docs/current/transaction-iso.html).
* Choosing a different level doesn't acquire any more locks
* It does have some performance implications
* More importantly, you will get serialization errors, and more ROLLBACKs.
* This could be a big deal depending on your system

#### Tests

* The presenter pointed out that the [tests for isolation levels](https://github.com/postgres/postgres/tree/master/src/test/isolation) are super cool, and recommended taking a look!
  * It has a README saying how to run the tests and add new ones

### Local-first application architecture using Postgres logical replication by Conrad Hofmeyr

* Goal: local-first architecture, where the user has all of their data on their local machine
  * Many interesting benefits for both end users and developers
  * Web examples of local-first: [excalidraw](https://excalidraw.com/) and [yjs](https://github.com/yjs/yjs)
    * And definitely electron applications too
* CouchDB has PouchDB, MongoDB has Realm?, which you can sync local to remote, nothing similar for Postgres
* Focus on SQLite since it is so heavily used in mobile apps
* They have a middleware for writes.  Logical replication writes from postgres to their middleware.  Clients authenticate to the middleware using JWTs, and add the data to a local SQLite database
* App will write new data to SQLite, and then the application must also sync back to Postgres
  * Interesting question: if you INSERT a record with a new id in SQLITE, then INSERT another row that refers to it, when it writes back to Postgres.  Answer: just use UUIDs. 

#### Challenges in using streaming replication

* Streaming replication is awesome and enabled this project
* Schema changes are a challenge -- to minimize the impact, the SQLite database is schemaless json
* Handling different row identifier information other than primary keys -- they recommend primary key

### Informally...

* pg collector seems like a really cool tool for monitoring/stats
