# MemoryDB

* in-memory database; upt to 100 TB

### Features
* Multi-availability zones
* transaction log for recovery and durability
* very fast; > 160 M requests/second
    * microsecond read latency
    * single-digit millisecond write latency

### Uses
* as ultra-fast, Redis-compatible primary database
* high performance apps needing an in-memory database to handle millions of requests per second
* apps that need to be data intensive, low latency, and higly scalable
* highly scalable microservices
* e.g online game with millions of users sharing digital assets
