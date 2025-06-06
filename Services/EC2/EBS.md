# Elastic Block Store (EBS)
* storage volumes (i.e disk) you can attach to EC2 instance
* EC2 instances typically come with 1 EBS to store the OS
* additional EBS can be attached to EC2 instance to store apps, data, etc.

### Pros
* highly available: automatically replicated within single availability zone
* scalable: can dynamically increase capacity and change volume type with no downtime or performance impact to live systems

### Types
* gp2: General Purpose SSD, balance of price and performance, 16 IOPS/GiB up to 16K IOPS per volume, gp2 volumes smaller than 1TB can burst up to 16K IOPS, good for boot volumes, apps that're not latency sensitive
* gp3: General Purpose, 
* io1: provisioned iops ssd, way more expensive than gp2 and gp3, high performance option, 64K IOPS per volume up to 16 TB, possibly legacy option, likely should use io2 instead for new instances
* io2 block express: provisioned iops ssd, even higher performance and durability than io1 for same price, for I/O intensive apps, large databases, latency and durability sensitive workloads
* st1: thoroughput optimized HDD, low cost HDD, good for storing a lot of data that needs to be accessed frequently (thorougput intensive), Big Data, data warehouses, ETL, log processing
* sc1: cold hdd, baseline throughput, good for apps that need low cost and performance isn't important


### IOPS (Inout/Output per second)
* measures number of read and write operations per second
* important for quick transactions, low latency apps, transactional workloads 

### Throughput
* measures number of bits read or written per second (MB/s)
* important for large datasets, large I/O ,complex queries 


### References

[EBS Types](https://docs.aws.amazon.com/ebs/latest/userguide/ebs-volume-types.html)

