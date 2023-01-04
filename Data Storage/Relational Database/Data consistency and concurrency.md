# Data Consistency

## PostgreSQL ([[Relationsal Database ManagementSystem]])
When data is modified, exclusive locks are set and held until the end of the transaction. For data consistency, PostgreSQL uses a [[Multi-Version Concurrency Control (MVCC)|multi-version consistency model]]: A copy of the original row is kept for readers before performing writer modifications. Readers do not have to wait for writers as in Informix. The simplest way to think of the PostgreSQL implementation of read consistency is to imagine each user operating a private copy of the database, hence the multi-version consistency model. The lock wait mode cannot be changed as in Informix. Locks are set at the row level in PostgreSQL and this cannot be changed.

