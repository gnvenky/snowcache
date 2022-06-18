# snowcache
A cache made for snowflake


Built on top of the versatile RocksDB, this cache in language 'TBD' will work seamlessly with 
Snowflake. The intent is to make it work transparently with any snowflake instance.

Snowflake should be able to work seamlessly with the Cache.
A read through cache is useful for read intensive workloads after the cache is warmed up.
On a write of the object, the cache entries are set to dirty, and fetched from source before
clearing the dirty bit on the next read.

There will also be a refresh-ahead strategy built around least recently used blocks, for 
which there will be separate task spawned on a read that will happen in a designated interval
that will help in write intensive scenarios.

The main cache will be coded in 'Python'/ 'Go'
