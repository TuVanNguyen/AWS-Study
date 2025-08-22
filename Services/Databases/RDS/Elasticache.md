# Elasticache

Purpose: speed up database read queries by storing frequently accessed data in a cache

### How it works
* key-value data store
* acts as an in-memory cache in cloud, bypassing need to access the slower disk-based storage

### When to Use
* read-heavy workloads
* data not prone to freqent changing i.e infrequent writes 

### When not to Use
* write heavy workloads because elasticache can end up with outdated info
    * instead, consider scaling up database
* database stress is coming from OLAP (Online Analytical Processing) queries
    * need a data warehouse like Redshift


## Types 

### Memcached
* great for basic, simple object caching
* scales horizontally
* no persistence, multi-availability zones, or failover

### Redis
* has persistence, replication, multi-availability zones, failover
* supports ranking and sorting data
* support complex data types e.g lists, hashes
* for more complex situations
