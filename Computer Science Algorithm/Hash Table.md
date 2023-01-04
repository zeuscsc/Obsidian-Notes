
---
cssClass:
- cards
- cards-1-1
- img-grid
---

In computing, a hash table, also known as hash map, is a data structure that implements an associative [[array]] or dictionary. It is an abstract data type that maps keys to values. A hash table uses a [[hash function]] to compute an index, also called a hash code, into an [[array]] of buckets or slots, from which the desired value can be found. During lookup, the key is hashed and the resulting hash indicates where the corresponding value is stored.

![[Pasted image 20230104111458.png]]|![[Pasted image 20230104111527.png]]
-|-
A small phone book as a hash table|Hash collision resolved by separate chaining
![[Pasted image 20230104111600.png]]|![[Pasted image 20230104111627.png]]
Hash collision by separate chaining with head records in the bucket [[array]].|Hash collision resolved by open addressing with linear probing (interval=1). Note that "Ted Baker" has a unique hash, but nevertheless collided with "Sandra Dee", that had previously collided with "John Smith".

