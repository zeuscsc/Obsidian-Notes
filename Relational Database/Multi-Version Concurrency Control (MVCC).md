# Wiki Definiation
Multiversion concurrency control (MCC or MVCC), is a concurrency control method commonly used by database management systems to provide concurrent access to the database and in programming languages to implement transactional memory.

# What it does
The DBMS maintains multiple physical versions of a single logical object in the database
When a Transaction writes to an object, the DBMS creates a new version of that object.
When a Transaction reads an object, it reads the newest version that existed when the txn started.
## In other words
Writers don't block readers. Readers don't block writers.
Read-only Transactions can read a consistent snapshot without acquiring locks.

---

### Case 1
Clock|Snapshots|${\displaystyle T_{1}}$ Timestamp=1|${\displaystyle T_{2}}$ Timestamp=2
-|-|-|-
0|1||&nbsp;
1|1|Begin|&nbsp;
2|1|R(A)|Begin
3|2&rarr;3|&nbsp;|W(A)
4|3|R(A)|💾
5|3|Commit|💾
6|3||Commit

0. The database start like snapshot 1
1. Begining of Transcation 1 (${\displaystyle T_{1}}$).
2. When ${\displaystyle T_{1}}$ read database, it get 123 accroding to snapshot 1.
3. Beginning of Transaction 2 (${\displaystyle T_{2}}$).
4. ${\displaystyle T_{2}}$ Create version ${\displaystyle A_{1}}$ and sets ${\displaystyle A_{0}}$ end-timestamp.
5. ${\displaystyle T_{1}}$ read version ${\displaystyle A_{0}}$.

#### Database Snapshot 1
Version|Value|Begin|End
-|-|-|-
${\displaystyle A_{0}}$|123|0|${\displaystyle \infty}$

#### Database Snapshot 2
Version|Value|Begin|End
-|-|-|-
${\displaystyle A_{0}}$|123|0|${\displaystyle \infty}$
${\displaystyle A_{1}}$|456|2|${\displaystyle \infty}$

#### Database Snapshot 3
Version|Value|Begin|End
-|-|-|-
${\displaystyle A_{0}}$|123|0|2
${\displaystyle A_{1}}$|456|2|${\displaystyle \infty}$

Transraction id|Timestamp|Status
-|-|-
${\displaystyle T_{1}}$|1|Active
${\displaystyle T_{2}}$|2|Active

---

### Case 2
Clock|Snapshots|${\displaystyle T_{1}}$ Timestamp=1|${\displaystyle T_{2}}$ Timestamp=2
-|-|-|-
0|1||&nbsp;
1|1|Begin|&nbsp;
2|1|R(A)|Begin
3|2|W(A)|&nbsp;
4|3|💾|R(A)
5|3|💾|W(A)
6|3|R(A)|⏳
7|4|COMMIT|⏳
8|5||💾
9|5||💾
10|6||COMMIT

0. The database start like snapshot 1.
1. Begining of Transcation 1 (${\displaystyle T_{1}}$).
2. When ${\displaystyle T_{1}}$ read database, it will get  ${\displaystyle A_{0}}$ (123), clock 2 is also the begining of Transcation 2 (${\displaystyle T_{2}}$).
3. ${\displaystyle T_{1}}$ start writing things to database, add a version ${\displaystyle A_{1}}$ and set ${\displaystyle A_{0}}$ end-timestamp.
4. ${\displaystyle T_{2}}$ read from database, it will get results from  ${\displaystyle A_{0}}$ because  ${\displaystyle T_{1}}$ has not committed yet.
5.  ${\displaystyle T_{2}}$ want to write things to database, but has to stall until ${\displaystyle T_{1}}$ commits.
6.  ${\displaystyle T_{1}}$ read database, it will get  ${\displaystyle A_{1}}$ (456) that it wrote earlier.
7. Change the status of  ${\displaystyle T_{1}}$  to committed.  
8. Now ${\displaystyle T_{2}}$ create the new version
9.  ${\displaystyle T_{2}}$ saving
10. Change the status of  ${\displaystyle T_{2}}$  to committed.  

#### Database Snapshot 1
Version|Value|Begin|End
-|-|-|-
${\displaystyle A_{0}}$|123|0|${\displaystyle \infty}$

#### Database Snapshot 2
Version|Value|Begin|End
-|-|-|-
${\displaystyle A_{0}}$|123|0|1
${\displaystyle A_{1}}$|456|1|${\displaystyle \infty}$

Transraction id|Timestamp|Status
-|-|-
${\displaystyle T_{1}}$|1|Active


---

#### Database Snapshot 3
Version|Value|Begin|End
-|-|-|-
${\displaystyle A_{0}}$|123|0|1
${\displaystyle A_{1}}$|456|1|${\displaystyle \infty}$

Transraction id|Timestamp|Status
-|-|-
${\displaystyle T_{1}}$|1|Active
${\displaystyle T_{2}}$|2|Active



---



#### Database Snapshot 4
Version|Value|Begin|End
-|-|-|-
${\displaystyle A_{0}}$|123|0|1
${\displaystyle A_{1}}$|456|1|${\displaystyle \infty}$

Transraction id|Timestamp|Status
-|-|-
${\displaystyle T_{1}}$|1|Committed
${\displaystyle T_{2}}$|2|Active



---
#### Database Snapshot 5
Version|Value|Begin|End
-|-|-|-
${\displaystyle A_{0}}$|123|0|1
${\displaystyle A_{1}}$|456|1|2
${\displaystyle A_{2}}$|789|2|${\displaystyle \infty}$

Transraction id|Timestamp|Status
-|-|-
${\displaystyle T_{1}}$|1|Committed
${\displaystyle T_{2}}$|2|Active



---
#### Database Snapshot 6
Version|Value|Begin|End
-|-|-|-
${\displaystyle A_{0}}$|123|0|1
${\displaystyle A_{1}}$|456|1|2
${\displaystyle A_{2}}$|789|2|${\displaystyle \infty}$

Transraction id|Timestamp|Status
-|-|-
${\displaystyle T_{1}}$|1|Committed
${\displaystyle T_{2}}$|2|Committed



---



### Other Demo
There is mainly 3 stages for MVCC
1. Simulation
2. Validation
3. Commit



Time|Phase|Transaction 1|Transaction 2|Phase
-|-|-|-|-
1|&nbsp;|&nbsp;|read(id=1)|Simulation
2|Simulation|read(id=1)|&nbsp;|Simulation
3|Simulation|&nbsp;|write(id=2)|Simulation
4|Simulation|&nbsp;|&nbsp;|Validation
5|Simulation|&nbsp;|commit|Commit
6|Simulation|write(id=2)|&nbsp;|&nbsp;
7|Validation|&nbsp;|&nbsp;|&nbsp;
8|&nbsp;|commit|&nbsp;|&nbsp;
9|&nbsp;|❌ will not commit|✔ will commit|&nbsp;

At the begining, Transaction 2 arrive the database engine first, it enter the simulation phase by reading the current id from the harddisk.  Then Transaction 1 arrives and it read from the harddisk as well.  Since reading ([[Relationsal Database ManagementSystem#Select|Select]]) from harddisk is not locked, both Transactions will be able to read the id.  After both Transactions read the id, Transaction 2 start writing the id within the Simulation Phase.  After Transaction 2 simulated the write, it will go to Validation Phase for Transaction 2.  The database will ask a question, (Did other Transactions commit item 'id' while Transaction 2 is running?) For Transaction 2 the answer is no because it is the only Transaction that is going to commit up to this point.  After the Validation phase is also pass, the Transaction 2 will commit and store the new id value to harddisk.  When we look back into Transaction 1, the Simulation is still on going because Transaction 2 was writing the id into the harddisk.  After Transaction 2 done with the commit, Transaction 1 will start its Simulation for writing id.  When reaching Validation phase for Transaction 1, it will ask the same question as metion above.   (Did other Transactions commit item 'id' while Transaction 1 is running?)  This time, the answer will be yes.  It is because Transaction 2 has already successfully commit during the Simulation phase for Transaction 1.  That's why Transaction 1 will not commit.
This method is also belong to [[Snapshot Isolation]].


### Script Demo

~~~postgresql
CREATE DATABASE trx_demos;
DROP TABLE IF EXISTS txn_demo;
CREATE TABLE txn_demo(
	id INT PRIMARY KEY,
	val INT NOT NULL
);
INSERT INTO txn_demo VALUES (1,100),(2,200);
BEGIN TRANSACTION ISOLATION LEVEL READ COMMITTED;
SELECT * FROM txn_demo WHERE id=1;
SELECT xmin,xmax, * FROM txn_demo WHERE id=1;
SELECT txid_current();
UPDATE txn_demo SET val=val+1 WHERE id=1;
SELECT xmin,xmax, * FROM txn_demo WHERE id=1;
SELECT xmin,xmax,ctid, * FROM txn_demo WHERE id=1;
COMMIT;
SELECT xmin,xmax,ctid, * FROM txn_demo;
BEGIN TRANSACTION ISOLATION LEVEL SERIALIZABLE;
~~~


Transaction 1|Transaction 2
-|-
BEGIN TRANSACTION ISOLATION LEVEL SERIALIZABLE;|BEGIN TRANSACTION ISOLATION LEVEL READ COMMITTED;
UPDATE txn_demo SET val=val+1 WHERE id=1;|UPDATE txn_demo SET val=val+1 WHERE id=2;
SELECT xmin,xmax,ctid, * FROM txn_demo;|SELECT xmin,xmax,ctid, * FROM txn_demo;



