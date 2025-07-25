# Relational Database Service

### What
* Data organized into tables with rows and columns

### Use
* generally for Online Transaction Processing Workloads
    * large numbers of small transactions in real-time
    * e.g banking, payments, booking
* not recommended for Online Analytics Processing (OLAP)
    * process complex queries to analyze historical data
    * can take long to complete
    * e.g sales forecasting, data analytics
    * recommend use data warehouse like Redshift instead


### Features
* Multiple availabily zones: 
    * provides resilience, for disaster recovery
    * not for scaling out or improving performance
* read replicas
* failover capable
* automatic backups

### Types of RDS available
* Microsoft SQL Server
* Oracle
* MySQL
* PostgreSQL
* MariaDB
* Amazon Aurora

## Read Replicas
* Read replicas: read-only copies of primary database
    * great to take read-heavy workloads off your primary database
    * can use to separate business users' requests from app server requests
    * each read replica has its own DNS endpoint
    * can be promoted to be their own independent databases
    * use for scaling read performance
    * requires automatic backups
    * up to 5 replicas per database

## Backups
* snapshots are stored in s3
* get free storage space equal to size of database
* storage I/O may be suspended while backup process initializes, and experience latency
* restored version of database will always be new RDS instance with new DNS endpoint
* Encryption at rest
    * AES-256 encryption
    * done with AWS Key Management Service (KMS)
    * includes all DB storage: snapshots, backups, logs, read replicas
    * must be done on creation, can't later enable encryption on an unencrypted RDS DB instance
        * instead, take snapshot, then create encrypted snapshot, then do database restore using encrypted snapshot

### Database snapshots
* snapshot of storage volume attached to database
* manual, ad-hoc, user-initiated
* no retention period, no automatic deletion


### Automated Backup
* enabled by default
* creates daily backups or snapshots within a defined backup window
* also stores transaction logs to be then applied on recovery point
* point-in-time recovery: recover database within retention period of 1-35 days
    * RDS loads latest snapshot
    * RDS replays the transaction logs to apply changes that occur up to recovery point


## RDS Proxy
* receives traffic from client applications
* pools and shares database connections to assist with application scalability and database efficiency
* sends information from the client apps, to the RDS databases