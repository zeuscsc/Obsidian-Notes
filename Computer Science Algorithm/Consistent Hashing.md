## Introducing Hash Tables (Hash Maps)

Imagine we needed to keep a list of all the members of some club while being able to search for any specific member. We could handle it by keeping the list in an [[array]] (or [[linked list]]) and, to perform a search, iterate the elements until we find the desired one (we might be searching based on their name, for instance). In the worst case, that would mean checking all members (if the one we’re searching for is last, or not present at all), or half of them on average. In complexity theory terms, the search would then have complexity `O(n)`, and it would be reasonably fast for a small list, but it would get slower and slower in direct proportion to the number of members.

How could that be improved? Let’s suppose all these club members had a member `ID`, which happened to be a sequential number reflecting the order in which they joined the club.

Assuming that searching by `ID` were acceptable, we could place all members in an [[array]], with their indexes matching their `ID`s (for example, a member with `ID=10` would be at the index `10` in the [[array]]). This would allow us to access each member directly, with no search at all. That would be very efficient, in fact, as efficient as it can possibly be, corresponding to the lowest complexity possible, `O(1)`, also known as _constant time_.

But, admittedly, our club member `ID` scenario is somewhat contrived. What if `ID`s were big, non-sequential or random numbers? Or, if searching by `ID` were not acceptable, and we needed to search by name (or some other field) instead? It would certainly be useful to keep our fast direct access (or something close) while at the same time being able to handle arbitrary datasets and less restrictive search criteria.

Here’s where hash functions come to the rescue. A suitable [[hash function]] can be used to map an arbitrary piece of data to an integer, which will play a similar role to that of our club member `ID`, albeit with a few important differences.

First, a good [[hash function]] generally has a wide output range (typically, the whole range of a 32 or 64-bit integer), so building an [[array]] for all possible indices would be either impractical or plain impossible, and a colossal waste of memory. To overcome that, we can have a reasonably sized [[array]] (say, just twice the number of elements we expect to store) and perform a _modulo_ operation on the hash to get the [[array]] index. So, the index would be `index = hash(object) mod N`, where `N` is the size of the [[array]].

Second, object hashes will not be unique (unless we’re working with a fixed dataset and a custom-built [perfect [[hash function]]](https://en.wikipedia.org/wiki/Perfect_hash_function), but we won’t discuss that here). There will be _collisions_ (further increased by the modulo operation), and therefore a simple direct index access won’t work. There are several ways to handle this, but a typical one is to attach a list, commonly known as a _bucket_, to each [[array]] index to hold all the objects sharing a given index.

So, we have an [[array]] of size `N`, with each entry pointing to an object bucket. To add a new object, we need to calculate its `hash modulo N`, and check the bucket at the resulting index, adding the object if it’s not already there. To search for an object, we do the same, just looking into the bucket to check if the object is there. Such a structure is called a _[[hash table]]_, and although the searches within buckets are linear, a properly sized [[hash table]] should have a reasonably small number of objects per bucket, resulting in _almost_ constant time access (an average complexity of `O(N/k)`, where `k` is the number of buckets).

With complex objects, the [[hash function]] is typically not applied to the whole object, but to a _key_ instead. In our club member example, each object might contain several fields (like name, age, address, email, phone), but we could pick, say, the email to act as the key so that the [[hash function]] would be applied to the email only. In fact, the key need not be part of the object; it is common to store key/value pairs, where the key is usually a relatively short string, and the value can be an arbitrary piece of data. In such cases, the [[hash table]] or hash map is used as a _dictionary_, and that’s the way some high-level languages implement objects or associative arrays.

## Scaling Out: Distributed Hashing

Now that we have discussed hashing, we’re ready to look into _distributed hashing_.

In some situations, it may be necessary or desirable to split a [[hash table]] into several parts, hosted by different servers. One of the main motivations for this is to bypass the memory limitations of using a single computer, allowing for the construction of arbitrarily large hash tables (given enough servers).

In such a scenario, the objects (and their keys) are _distributed_ among several servers, hence the name.

A typical use case for this is the implementation of in-memory caches, such as [Memcached](https://en.wikipedia.org/wiki/Memcached).

Such setups consist of a pool of caching servers that host many key/value pairs and are used to provide fast access to data originally stored (or computed) elsewhere. For example, to reduce the load on a [[database]] server and at the same time improve performance, an application can be designed to first fetch data from the cache servers, and only if it’s not present there—a situation known as _cache miss_—resort to the [[database]], running the relevant query and caching the results with an appropriate key, so that it can be found next time it’s needed.

Now, how does distribution take place? What criteria are used to determine which keys to host in which servers?

The simplest way is to take the hash _modulo_ of the number of servers. That is, `server = hash(key) mod N`, where `N` is the size of the pool. To store or retrieve a key, the client first computes the hash, applies a `modulo N` operation, and uses the resulting index to contact the appropriate server (probably by using a lookup table of IP addresses). Note that the [[hash function]] used for key distribution must be the same one across all clients, but it need not be the same one used internally by the caching servers.

Let’s see an example. Say we have three servers, `A`, `B` and `C`, and we have some string keys with their hashes:

KEY|HASH|HASH mod 3
-|-|-
"john"|1633428562|2
"bill"|7594634739|0
"jane"|5000799124|1
"steve"|9787173343|0
"kate"|3421657995|2

A client wants to retrieve the value for key `john`. Its `hash modulo 3` is `2`, so it must contact server `C`. The key is not found there, so the client fetches the data from the source and adds it. The pool looks like this:

A|B|C
-|-|-
&nbsp;|&nbsp;|"john"

Next another client (or the same one) wants to retrieve the value for key `bill`. Its `hash modulo 3` is `0`, so it must contact server `A`. The key is not found there, so the client fetches the data from the source and adds it. The pool looks like this now:

A|B|C
-|-|-
"bill"|&nbsp;|"john"

After the remaining keys are added, the pool looks like this:
A|B|C
-|-|-
"bill"|"jane"|"john"
"steve"|&nbsp;|"kate"
