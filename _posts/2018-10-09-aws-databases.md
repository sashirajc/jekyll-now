---
layout: post
title: Databases on AWS
tags: AWS
---

Relational databases supported by AWS:
1. Microsoft SQL Server
2. MySQL
3. Aurora
4. Oracle
5. PostgreSQL
6. MariaDB

Non-relational databases supported by AWS:
1. DynamoDB

Datawarehousing

Used for business intelligence. Used to pull in very large and complex data sets. Usually used by management to do queries on data. Tools like Cognos, Jasperson, SQL Server Reporting Services, Oracle Hyperion, SAL Netweaver


OLTP - Online Transaction Processing
General queries to get value of something in the database


OLAP - Onlina Analytics Processing
Complex queries used to generate reports and other complicated analysis affecting multiple rows and columns. Typically run on a datawarehouse instead of directly running on production databases. Redshift is AWS's resource.

DataWarehousing databases use different type of architecture from a database perspective as well as infrastructure layer.

Elasticache

Webservice that deploys, operates and scales an in-memory cache on AWS. Improves the performance of web applications by allowing to cache and retrieve information from fast, managed, in memory caches. Both Memcached and Redis are supported.

## RDS

DB Identifier is a unique name to identify all databases owned by your account in the region.

Backups on AWS
1. Automated backups - Allow you to recover database to any point within a 'retention period'. Retention period can be between 1 to 35 days. Automated backup will take a full daily snapshot and will store transaction logs throughout the dat. To recover, AWS will choose the most recent daily backup and apply transaction logs relevant to that day. This allows to do a point in time recovery down to a second within the retention period.

Enabled by default. Backup is stored on S3 for free. Backups are taken within a defined window. During backup windows, storage I/O may be suspended while data is being backed up and may experience elevated latency.
They get deleted if the original RDS instance is deleted.

2. Snapshot - Snapshots are done manually (user initiated). Stored even after original RDS instance is deleted.

If backups are restored, it will have a new DNS and endpoint. So it is as good as a new database with the data of the old.

## Encryption

Encryption at rest is supported on all databases. Encryption is done using AWS Key Management Service. Once RDS is encrypted, data stored at rest in underlying storage is encrypted as well.

Encryption of existing DB instance is not supported. A snapshot can be taken and a copy of that snapshot can be encrypted and used as the new database.

## Multi AZ

Multi AZ allows to have an exact copy of production database in another availability zone. AWS handles the replication, so when production database is written to, this write will automatically be synchronized to the standby database. When a planned database migration or availability zone failure or db instance failure occurs, AWS RDS will automatically failover to the standby so that database operations can resume quickly without intervention.

Multi AZ is only for disaster recovery. For performance enhancement read replicas must be used.

Aurora does not have multi-az

Read replicas allow to have a read only copy of production database. This is achieved by using asynchronous replication from primary RDS instance to the read replica. Read replicas primarily are used for very read-heavy database workloads. They are used for scaling, not for disaster recovery.

Automatic backups must be turned on to deploy a read replica. Upto 5 read replica copies of database can be used. Read replicas can be made of other read replicas of the original database at the cost of additional latency.

Each read replica has its own endpoint

Read replicas can be on multiple -az and on other regions as well.

Read replicas can be promoted to be their own database at the cost of breaking the replication.

Oracle and SQL server do not have read replicas

## DynamoDB

Fast and flexible noSQL database service for applications that need consistent, single digit millisecond latency at scale. Fully managed database and supports document and key-value data models. Flexible datamodel and reliable performance.

Always stored on SSD storage.

Spread across 3 different distinct data centers.

Consistency levels:

1. Eventual consistent read

Consistency across all copies of data is usually reached within a second. Repeating a read after a short time should return the updated data.

2. Strongly consistent reads

Strongly consistent read returns a result that reflects all writes that received a successful response prior to the read.

Pricing based on provisioned throughput capacity.

## Redshift

Redshift is a fast and powerful, fully managed, petabyte scale data warehouse service in the cloud. 

Redshift can have a single node or a multi node. Multi-node can be of type leader node or compute node. Leader node, managesclient connections and receives queries. Compute node stores data and performs queries and computations. There can be upto 128 compute nodes.

Redshifts stores by columns which are ideal for data warehousing and analytics.

Advanced compression. Employs multiple compression techniques and can often achieve significant compression relative to traditional relation databases. Redshift doesnt require indexes or materialised views and so uses less space than traditional RDBMS. Compression scheme selection is automatically selected when loading data to empty table. Redshift samples the data to decide on the compression scheme.

Massive Parallel Processing - Automatically distributes data and query load across all nodes. Process of adding nodes to data warehouse is also easy and enables to maintain fast query performance as data warehouse grows.

Pricing - Charged for total number of hours across all compute nodes. Leader nodes are not charged. Charged for backup and for data transfer within VPC

Security - Encrypted at transit using SSL, Encrypted at REst using AES-256 encryption. Key management is done by AWS, but can also be managed from HSM.

Redshift can only be available on 1 az. Can restore snapshots to new az in the event of outage.

