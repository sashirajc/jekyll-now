---
layout: post
title: AWS Elastic Compute Cloud (EC2)
tags: AWS
---

Elastic Compute Cloud is a web service that provides resizable compute capacity in the cloud. EC2 reduces the time required to obtain and boot a new server instance to minutes, allowing to quickly scale capacity up and down based on requirements. 

EC2 changes the economics of computing by allowing to pay only for capacity instead of purchasing a new one. EC2 provides developers with the tools to build failure resilient applications and isolate themselves from common failure scenarios.

## Types of EC2 pricing

1. On Demand - allows you to pay a fixed rate by the hour (windows) or by second (linux). 

Use Cases - Perfect for users who want low cost and flexibility of EC2 without upfront payment or long term commitment. Applications with short term, spiky or unpredicatable workloads that cannot be interrupted. 

2. Reserved - provides with a capacity reservation and offers a discount on the hourly change for instance. Reserved instances are purchased over a term of 1 or 3 years with options to pay a percentage of the price upfront and the remaining every month or all upfront. Reserved instances can be upto 75% cheaper.

Use Cases: Applications with steady state or predictable usage. Applications that require reserved capacity. Users can make upfront payments to reduce their total computing costs with
- Standard RI (75% off)
- Convertible RI (54% off) these have the capacity to change the attributes of RI as long as the exchange results in creation of Reserved instances of greater or equal value.
- Scheduled RI are available to launch within the time window in which it is reserved. This option allows to match capacity reservation to a predictable recurring schedule that only requires a fraction of a day,week or month.

3. Spot - Enables to bid whatever price for instance capacity, providing for even greater savings if applications have flexible start and end times.

If a spot instance is terminated by Amazon EC2, you will not be charged for a partial hour of usage. However, if you terminate the instance yourself, you will be charged for the complete hour in which the instance ran.

Use Cases: 
Applications that have flexible start and end times.
Applications that are only feasible at very low compute prices.
Users with an urgent need for large amounts of compute capacity.

4. Dedicated hosts  - Physical EC2 server dedicated for your use. Dedicated hosts help to reduce costs by allowing to use existing software-bound licenses.

Use Cases: Useful for regulatory requirements that may not support multi-tenant virtualization.
Great for licenseing which does not support multi tenancy or cloud deployments.
Can be purchased on -demand or can also be reserved.

## EC2 Instance Types
* F - FPGA                       - Genomics Research, Big data
* I - IOPS                       - NoSQL, DataWarehousing
* G - Graphics                   - Video Encoding, 3D streaming
* H - High Disk Throughput       - MapReduce, HDFS
* T - General purpose (cheap)    - Web Servers
* D - Density                    - File Servers, Hadoop
* R - RAM                        - Memory intensive applications
* M - General purpose            - Application Servers
* C - Compute                    - CPU Intensive
* P - Graphics                   - Machine learning, bitcoin mining
* X - Extreme Memory             - SAP Hana

## Elastic Block Storage (EBS)

Amazon EBS allows to create storage volumes and attach to EC2 instances. Once attached, it can create a file system on top of these volumes, run a database or use in any other way. EBS volumes are placed in a specific availability zone where they are automatically replicated to protect from failure of a single component.

## EBS Volume types

* General Purpose SSD (GP2)
Balances both price and performance.
Ratio of 3 IOPS per GB with upto 10,000 IOPS and ability to burst up to 3000 IOPS for extended periods of time for volumes at 3334 GiB and above.

* Provisioned IOPS SSD(IO1)
Designed for IO intensive applications such as databases. Use if you need more than 10,000 IOPS
Can provision upto 20,000 IOPS per volume

* Throughput Optimized HDD(ST1)
Big data, data warehousing, log processing. These cannot be a boot volume

* Cold HDD (SC1)
File server, cannot be boot volume, lowest cost storage for infrequently accessed workloads

* Magnetic (Standard)
Lowest cost per gb for all EBS volume types that is bootable. Magnetic volumes are ideal for worklaods where data is accessed infrequently and applications where the lowest storage cost is important.

EC2 instance and EBS volume must be on the same availability zone. They cannot be in a different availability zone.
An EBS volume can be moved to a different availability zone by creating a snapshot and using the snapshot to create a volume in another availability zone.

Snapshot can also be copied to a new region. A new volume can be created from the snapshot and attached to a new EC2 instance on the other region.

Images can also be created which can be used to create AMIs. AMIs can be used to create new EC2 instances which will have all the data in the volume from which the image was taken.

Snapshots are used for backups. Images are used to create new EC2 instances.

Snapshots are stored on S3. But not accessible on S3 buckets.

Snapshots are point in time copies of volumes. They are incremental - only blocks that have changed from the previous snapshot is stored. First snapshots take sometime to get created.

Snapshots on root devices can only be taken after stopping the instance. AMIs can be created from both snapshots and EBS backed instances.

EBS volume types can be changed on the fly and size and storage types can be changed.

Snapshots of encrypted volumes are automatically encrypted.

Volumes restored from encrypted snapshots are automatically encrypted.

Snapshots can be shared if they are unencrypted. They can be shared with other AWS accounts or made public.

## RAID, Volumes and Snapshots

RAID = Redundant Array of Independent Disks

RAID 0 - Striped, No Redundancy, Good Performance
RAID 1 - Mirrored, Redundancy
RAID 5 - Good for reads, bad for writes, not recommended by AWS
RAID 10 - Striped and Mirrored, Good redundancy and performance

RAID arrays are used when the disk IO is not satisfactory. When there is a single volume and it is provisioned to maximum size. Solution is to create multiple volumes and create RAID arrays to give the I/O that is required. 

To take a snapshot of a RAID disk, there should be no data on caches, which is difficult on RAID due to interdependencies. 

This can be solved by - 
1. Stop the application from writing to disk
2. Flush all caches to disk

This can be done either by 
Freezeing the file system or unmounting the RAID array or shutting down the associated EC2 instance and then take a snapshot.

## Notes

1 subnet can only exist in 1 availability zone. You cannot have a subnet that goes across more than 1 availability zone

Security group is a firewall. Firewall can be configured to allow only certain types of connections from different IP address. Ex- Port 80 can be accessed by everyone on the web. But port 22 can only be accessed by a trusted IP address. (Port 80 is the HTTP port while 22 is SSH port giving terminal access)

Termination protection is turned off by default. 

On an EBS backed instance, the default action is for the root EBS volume to be deleted when the instance is terminated.

EBS Root Volumes of default AMIs cannot be encrypted. Third party tools can be used to encrypt the root volume or new AMIs can be created which already have encrypted root volumes.

Additional volumes can be encrypted at the time of instance creation

As a best practice, EC2 instances should be stopped before taking a snapshot of a root volume to avoid inconsistencies in the data.

Snapshots of encrypted volumes are encrypted automatically.

Volumes restored from encrypted snapshots are automatically encrypted.

Snapshots can be shared, only if they are unencrypted.

AMIs can be selected based on Architecture, Region, Operating System, Launch Permissions and Storage for Root Device -Instance Store or Ephemeral storage and EBS backed volumes.

Instance store - Instance store cannot be encrypted even if it is not a root. Root device for an instance launched from AMI is an instance store volume created from a template stored in S3. Instance store volumes are also called ephemeral storage. They cannot be stopped. If the underlying host fails you will lose all the data.

EBS Backed Store - Root device for an instance launched from an AMI is an Amazon EBS volume created from an Amazon EBS snapshot. EBS backed stores, can be stopped. Data will not be lost. 

Both instance store and EBS store based EC2 instances can be rebotted without losing the data. By default both root volumes will be deleted on termination, but with EBS volumes, AWS provides an option to keep the root device volume.

# EC2 Security Groups

Security group is a virtual firewall. 1 instance can have multiple security group. It is the first line of defence against hackers.

Any changes made to security groups will take effect immediately.

Security groups are stateful. Any request that goes in will also be allowed out. A HTTP request that goes in will also be allowed to go out even if it is not explictly mentioned in the outbound rules.

Adding an inbound rule, automatically adds an outbound rule.

All ports and types of traffic are blocked by default. Security groups only allow us to turn it on as needed. Traffic cannot be denied, it can only be allowed. They are denied on all ports by default.

More than one security group can be assigned to the same instance.

More than one instance can be within a security group.

Network access control lists are stateless. They can be used to block off individual IP addressess.

## Load Balancing

A virtual machine which can balance the load/traffic between multiple instances.

Types of load balancers

1. Application Load Balancer - Best suited for load balancing of HTTP and HTTPS traffic. They operate at Layer 7 and are application-aware. They are intelligent and can create advanced request routing, sending specified requests to specific web servers.

2. Network load balancer - Best suited for load balancing TCP traffic where extreme performance is required. Operating at connection level, network load balancers are capable of handling millions of requests per second while maintaining ultra low latencies. Used for extreme performance.

3. Classic load balancer - Legacy elastic load balancers. Can load balance HTTP/HTTPS applications and use layer 7 specific features such as X-Forwarded and sticky sessions. Can also use strict Layer 4 load balancing for applications that rely purely on TCP protocol.

Load balancer errors - 

Classic load balancer (ELB)  - If application stops responding, ELB responds with 504 error. Gateway has timed out. Application has stopped responding within the idle timeout period. This means web application is having issues at either web server layer or the database layer. Identify where the application is failing, and scale up or out where possible.

Forwarded-For header : Load balancer takes a IP address and adds the public IP address to the X-Forwarded-For header.

AWS managed the public IP address of the load balancer and only exposes the public DNS name. The public IP address may change.

## Cloudwatch

Monitoring and alerting service
Standard monitoring monitors every 5 mins. Detailed monitoring will drop it down to every 1 minute.

Dashboards - Create dashboards to monitor events happening with AWS resources.
Alarms - Alarms will notify you when certain thresholds are hit. This can be configured depending on which thresholds we want to monitor.
Events - Events help to respond to state changes in AWS resources.
Metrics - 
Logs - Aggregate, monitor and store logs by installing agents on EC2

Cloudwatch is for logging and performance monitoring
Cloudtrail is for monitoring user actions and auditing operations on entire AWS environment.

## AWS IAM Roles
AWS CLI needs programmatic access to provision resources and perform other operations from the CLI. But AWS CLI credentials are by default stored in the root folder in plaintext and this could be a huge security risk. To overcome this security risk, IAM roles can be used to manage user access programmatically.

IAM roles are global. IAM roles can be added/removed on running instances.

When accessing S3 buckets from AWS CLI, it is good practice to always mention the region flag. 

## Bash Script

A script that can be used to do some operations on EC2 when the instance is provisioned or turned on. Like boot scripts.

To check metadata of EC2 instance  - http://169.254.169.254/latest/meta-data

[Instance Metadata](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-metadata.html)

## Launch Configuration and AutoScaling

Before creating an autoscaling group, a launch configuration must be created. Autoscaling groups can be triggered by cloudwatch alarms. Extra instances can be added when the cpu utilization or another metric goes beyond a certain level.

Placement Groups - 
1. Clustered placement group
2. Spread placement group

Cluster placement group is a grouping of instances within a single availability zone. Placement groups are recommended for applications that need low network latency, high network throughput or both. By default placement groups refers to clustered. Only some instance groups can be inside a clustered placement group.

Spread placement group is a group of instances that are each placed on distinct underlying hardware. Spread placement groups are recommended for applications that have a small number of critical instances that should be kept separate from each other.They can be on separate availability zones.

AWS recommends homogenous instances within placement groups. Placement groups cant be merged. Existing instances cant be moved into a placement group. An AMI can be created from an existing instance and then launched as a new instance into the placement group.

## Elastic File System

File storage service for EC2 instances. Easy to use and provides a simple interface that allows to create and configure file systems quickly and easily. With EFS, storage capacity is elastic, growing and shrinking automaticaly as files are added or removed.

Supports NFSv4 protocol.
Only paid for storage that is used.
Can scale upto petabytes.
Can support thousands of concurrent NFS connections. 
Data is stored across multiple availability zone.
Read after write consistency.
Block based storage, not object based.

Unlike EBS volumes, EFS can be attached to more than one EC2 instance at once. It is a centralised repository for all files.

Read more from FAQs for this.

## Lambda

AWS Lambda is a compute service where code can be uploaded to create a lambda function. AWS Lambda takes care of provisioning and managing the servers needed to run the code.

It can be used as -
1. As an event driven compute service where AWS Lambda runs code in response to events. These events could be changes to date in an S3 bucket or DynamoDB table etc.
2. As a compute service to run code in response to HTTP requests using API Gateway or API calls made by AWS SDKs.

Lambda function cannot run for more than 5 minutes.

Advantages - no servers
continous scaling, extremely cheap

1 lambda function can trigger other lambda functions.
Debugging can be a nightmare, X-ray will be needed to debug problems.
Lambda can do things globally.

