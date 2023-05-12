### Definiation
A deadlock is a situation in which two computer programs sharing the same resource are effectively preventing each other from accessing the resource, resulting in both programs ceasing to function. The earliest computer operating systems ran only one program at a time.

![[Pasted image 20220725214424.png]]

### What it have to do with [[Relationsal Database ManagementSystem]]
In a [[database]], a deadlock is an unwanted situation in which two or more transactions are waiting indefinitely for one another to give up locks. Deadlock is said to be one of the most feared complications in DBMS as it brings the whole system to a Halt. 
When you tries to insert or update data on [[database]], sometime your record need to depend on the row record.  For example, when you insert the data with a auto increase id, both thansaction can't insert the same time or the data cannot keep its [[Data consistency and concurrency|consistency and concurrency]].  One way to keep the [[Data consistency and concurrency]] is to use [[Multi-Version Concurrency Control (MVCC)]] model but that could create another problem which is [[Deadlock]].



## Demo 1
~~~shell
psql -U postgres -W
~~~
~~~postgresql
\c trx_demos
CREATE DATABASE trx_demos;
DROP TABLE IF EXISTS txn_demo;
CREATE TABLE txn_demo(
	id INT PRIMARY KEY,
	val INT NOT NULL
);
INSERT INTO txn_demo VALUES (1,100),(2,200);
~~~


Clock|Transaction 1|Transaction 2
-|-|-
1|BEGIN TRANSACTION ISOLATION LEVEL READ COMMITTED;|&nbsp;
2||BEGIN TRANSACTION ISOLATION LEVEL READ COMMITTED;
3|SELECT xmin,xmax,ctid, * FROM txn_demo WHERE id=1 FOR UPDATE;|&nbsp;
4||SELECT xmin,xmax,ctid, * FROM txn_demo WHERE id=2 FOR UPDATE;
5|UPDATE txn_demo SET val=val+1 WHERE id=2;|&nbsp;
6||UPDATE txn_demo SET val=val+1 WHERE id=1;

~~~postgresql
SELECT xmin,xmax,ctid, * FROM txn_demo;
~~~
~~~postgresql
COMMIT;
~~~
~~~postgresql
SELECT xmin,xmax,ctid, * FROM txn_demo;
~~~

## Demo 2
~~~shell
psql -U postgres -W
~~~
~~~postgresql
\c trx_demos
CREATE DATABASE trx_demos;
DROP TABLE IF EXISTS txn_demo;
CREATE TABLE txn_demo(
	id INT PRIMARY KEY,
	val INT NOT NULL
);
INSERT INTO txn_demo VALUES (1,100),(2,200);
~~~


Clock|Transaction 1|Transaction 2
-|-|-
1|BEGIN TRANSACTION ISOLATION LEVEL READ COMMITTED;|&nbsp;
2||BEGIN TRANSACTION ISOLATION LEVEL READ COMMITTED;
3|INSERT INTO txn_demo (id,val) VALUES (1,100) ON CONFLICT (id) DO UPDATE SET val=101 RETURNING id;|&nbsp;
4||INSERT INTO txn_demo (id,val) VALUES (2,100) ON CONFLICT (id) DO UPDATE SET val=102 RETURNING id;
5|INSERT INTO txn_demo (id,val) VALUES (1,100) ON CONFLICT (id) DO UPDATE SET val=101 RETURNING id;|&nbsp;
6||INSERT INTO txn_demo (id,val) VALUES (2,100) ON CONFLICT (id) DO UPDATE SET val=102 RETURNING id;
7|UPDATE txn_demo SET val=val+1 WHERE id=2;|&nbsp;
8||UPDATE txn_demo SET val=val+1 WHERE id=1;

~~~postgresql
SELECT xmin,xmax,ctid, * FROM txn_demo;
~~~
~~~postgresql
COMMIT;
~~~
~~~postgresql
SELECT xmin,xmax,ctid, * FROM txn_demo;
~~~


## Quick copy
~~~shell
psql -U postgres -W
~~~
~~~postgresql
\c trx_demos
~~~
~~~postgresql
CREATE DATABASE trx_demos;
DROP TABLE IF EXISTS txn_demo;
CREATE TABLE txn_demo(
	id INT PRIMARY KEY,
	val INT NOT NULL
);
INSERT INTO txn_demo VALUES (1,100),(2,200);
~~~
~~~postgresql
BEGIN TRANSACTION ISOLATION LEVEL READ COMMITTED;
~~~
~~~postgresql
INSERT INTO txn_demo (id,val) VALUES (1,100) ON CONFLICT (id) DO UPDATE SET val=101 RETURNING id;
~~~
~~~postgresql
INSERT INTO txn_demo (id,val) VALUES (2,100) ON CONFLICT (id) DO UPDATE SET val=102 RETURNING id;
~~~
~~~postgresql
INSERT INTO txn_demo (id,val) VALUES (3,100) ON CONFLICT (id) DO UPDATE SET val=103 RETURNING id;
~~~
~~~postgresql
SELECT xmin,xmax,ctid, * FROM txn_demo;
~~~
~~~postgresql
commit;
~~~

## Interview Question
~~~postgresql
DROP TABLE IF EXISTS orders;
DROP TABLE IF EXISTS products;
CREATE TABLE products (  
id serial PRIMARY KEY,  
name VARCHAR(255) NOT NULL,  
quota INT NOT NULL DEFAULT 0
);
CREATE TABLE orders (  
id serial PRIMARY KEY,  
user_name VARCHAR(255) NOT NULL,  
product_id INT NOT NULL,  
product_name VARCHAR(255) NOT NULL,
FOREIGN KEY (product_id) REFERENCES products (id)  
);
insert into products (id,name,quota) values (456,'Hello World',10);
~~~
~~~postgresql
BEGIN TRANSACTION ISOLATION LEVEL READ COMMITTED;
~~~
~~~postgresql
INSERT INTO orders (user_name, product_id, product_name) SELECT 'Alex', id, name FROM products WHERE id = 456;
~~~
~~~postgresql
UPDATE products SET quota = quota - 1 WHERE id = 456;
~~~
~~~postgresql
commit;
~~~