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

This will also prevent the roundtrips to the Snowflake SAS endpoint.
The snowflake python connector and jdbc driver will have the capability to lookup cache
before making a roundtrip to the snowflake instance. 

Steps:

1. Augment the snowflake-jdbc driver to pull the request from Redis for any given query_id. Let Redis be a locally running instance.

2. Later. substitute the Redis with a redis backed with rocks-db. the redis dialect to support will only be SET, GET and possibly diagnostics
for this cache.

3. Test connections and data and publish some benchmarks.

![image](https://user-images.githubusercontent.com/277965/174487576-9182b029-6219-4540-b110-1d238ce3ca4b.png)
