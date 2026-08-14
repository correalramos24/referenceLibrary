# AWS Databases
- [AWS Databases](#aws-databases)
  - [Relational Database Service (RDS)](#relational-database-service-rds)
    - [Auto-scaling storage](#auto-scaling-storage)
    - [RDS Read-replicas \& multi-AZ](#rds-read-replicas--multi-az)
  - [Amazon Aurora (SQL)](#amazon-aurora-sql)
    - [Backup \& cloning](#backup--cloning)
    - [Security](#security)
    - [Proxy](#proxy)
  - [ElastiCache](#elasticache)
  - [DynamoDB](#dynamodb)
    - [DynamoDB Accelerator (DAX)](#dynamodb-accelerator-dax)
    - [DynamoDB Streams processing](#dynamodb-streams-processing)
  - [DocumentDB](#documentdb)
  - [Neptune](#neptune)
  - [Amazon Keyspaces (for Apache Cassandra)](#amazon-keyspaces-for-apache-cassandra)
  - [Timestream](#timestream)

## Relational Database Service (RDS)
Create & manage databases in the cloud which uses SQL as query language. 

It uses EBS as storage backend and the service is managed by AWS. There are many SQL engines available:
* Postgres
* MySQL
* Oracle & Microsoft SQL (RDS Custom, allows internal settings as a EC2 instance)
* MariaDB
* IBM DB2
* Aurora (AWS proprietary DB)

### Auto-scaling storage
Increase storage on your RDS DB dynamically. It is required to set a max. storage threshold.

### RDS Read-replicas & multi-AZ
Read replicas are used to scale the read operations (up to 15 replicas) within an AZ, cross AZ or Cross region.

* Replicas are ASYNC, providing eventually consistent.
* Is used to read-only uses cases in parallel with the production app.
* Read replicas only can do SELECT operations.
* RDS read replicas within the same region no extra cost is payed but across regions it has an extra fee.

RDS multi AZ is used for disaster recovery, using SYNC replication. This allows automatic failover. Behind the scenes RDS will have under the same DNS a master and a standby instance.

## Amazon Aurora (SQL) 
Proprietary tech from AWS but compatible drivers with MySQL/Postgres. Aurora storage automatically grows in increments of 10 GiB but it costs 20% more than RDS.

* It provides more performance than the others engines.
* 6 copies of your data across 3 AZs
  * 4/6 need for writes
  * 3/6 need for reads
  * Up to 15 read-replicas (which can become a master if failover)
* It Supports cross region replication.
* Auto scaling aurora replicas can be activated
* Custom endpoints of read-replicas for specific queries.
* Aurora serverless is used to automate DB instatiation & autoscaling. Used for unpredictable workloads.
* Aurora Global DB has a primary region but can set up to 10 secondary regions (with replication lag <1s). Cross-region replicaiton takes less than 1s.
* Babelfish is used to understand commands from other SQL engines (app drivers).

Aurora is also built to allow Machine learning services (Amazon SageMaker & Comprehend services). Used for product recommendations.

### Backup & cloning
Automated backups (daily) + transactions logs every 5 minutes + 1 to 35 days of retention (cannot be disabled in Aurora).

Is possible to generate manual DB snapshots. As an stopped DB will be paid per storage is useful to do this snapshots.

Anytime you restore/backup it creates a new database. Amazon S3 (buckets) can be used to restore a database.

Aurora DB can be cloned from an existing one (faster than a snapshot & restore as it uses CoW)

### Security
Uses AWS KMS for encryption. If the master is not encrypted the read replicas cannot be encrypted.

In-flight encryption (by default) using TLS security. IAM roles can be used to connect to your database.

Security groups can be used as well here.

Audit logs can be enabled via CloudWatch logs.

### Proxy
Improve the database efficiency by reducing the stress on the DB resources using a RDS Proxy. 

* Allows apps to pool & share DB connections.
* It enforces IAM auth.
* uses a serverless, autoscaling & high available service. It Reduces RDS & Aurora failover time by 66%.
* This proxy must be accessed form VPC (virtual private cloud). Usefull to use via lambda functions.

## ElastiCache
In-memory-databases use case service(valkey/redis,memcached).

It requires to changes your application source code (fill the ElastiCache in a cache miss from the RDS)

This services fills into the use cases to make application stateless.

Different patterns for use ElastiCache:
* Lazy loading: On the case of miss, retrive the data and store in the cache.
* Write through: All cache data is stored in RDS.
* Session store: Temp data.

Redis is very useful because of the sortedSet capability (create leaderboards)

NON-SQL! key-value scheme 

## DynamoDB
NoSQL Fully managed, highly availabile with replication across multiple AZs, scales to massive workloads (as it is a distributed databases) and has fast & consistent in performance. Usefull for rapidly evolve schemas. millisecond latency.

It has low cost and auto-scaling capabilities.

Each table has a primary key (decided at creation time) and infinite number of items (rows). Each items has attributed (can be added over time) and the max size is 400KB

Capacity modes:
1. Provisioned mode (default): read/write in advance & you pay for the RCU and WCU. Can be aut-scaling mode. Usefull for predictable workloads.
2. On-demand: More expensive but useful for unpredictable workloads & steep sudden spikes.

Items can be deleted after an expiry timestamp (TTL). 

DyamoDB can be exported/imported to/from S3 (requires Point-in-time-recovery PITR). Useful to query the bucket with Athena. 

### DynamoDB Accelerator (DAX)
Seanless in-memory cache for DyamoDB. Achieve microseconds latency for cached data. It is transparent to the programming logic.

Default 5mins TTL.

### DynamoDB Streams processing
Ordered stram of item-level modifications in a table (triggers).

It can be a kisesis data streams for the same use case but DynamoDB allows to have a processing layer to invoke a lambda function or use a KCL adapter.

## DocumentDB
Same as MongoDB(noSQL database) used to store, query and index JSON data.

## Neptune
Fully managed graph database.

It also have real-time ordered & no-duplicated sequence streams to be access via HTTP REST API. Also used to replicate data across regions in Neptune.

## Amazon Keyspaces (for Apache Cassandra)
NoSQL distributed database which is serverless, scalable & highly available.

On-demand & provisioned mode + auto-scaling

## Timestream
Fuly managed, fast and scalable time-series database. It is 100s faster and 1/10th cost of a full relational databases. Store & analyze trillions of events per day.

Comes from built-in time series analytics.

Can be used with Grafana/SageMaker/JDBC connection.