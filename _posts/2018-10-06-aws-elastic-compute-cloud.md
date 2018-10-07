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

## Notes

1 subnet can only exist in 1 availability zone. You cannot have a subnet that goes across more than 1 availability zone

Security group is a firewall. Firewall can be configured to allow only certain types of connections from different IP address. Ex- Port 80 can be accessed by everyone on the web. But port 22 can only be accessed by a trusted IP address. (Port 80 is the HTTP port while 22 is SSH port giving terminal access)

Termination protection is turned off by default. 

On an EBS backed instance, the default action is for the root EBS volume to be deleted when the instance is terminated.

EBS Root Volumes of default AMIs cannot be encrypted. Third party tools can be used to encrypt the root volume or new AMIs can be created which already have encrypted root volumes.

Additional volumes can be encrypted at the time of instance creation