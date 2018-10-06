---
layout: post
title: AWS Storage Gateway
tags: AWS
---

AWS Storage Gateway is a service that connects an on-premises software appliance with cloud-based storage to provide seamless and secure integration between an organisation's on-prem IT environment and AWS's cloud storage infrastructure. The service enables you to securely store data to the AWS cloud for scalable and cost-effective storage.

AWS Storage Gateway is available for download as a virtual machine image that can be installed in the datacenter. Storage gateway supports ESXi and Microsoft Hyper-V. Once the gateway is installed and associated with your AWS account, it can be used to the storage gateway type that you need.

## Types of Storage Gateways
1. File Gateway (NFS) - Store flat files such as PDFs, videos, pictures etc. Stored directly on S3. Files are assessed through a NEtwork File System (NFS) mountpoint. Ownership, permissions and timestamps are durably stored in S3 in the user-metadata of the object associated with the file. Once objects are transferred to S3, they can be managed as native S3 objects and bucket policies such as versioning, lifecycle management and cross-region replication apply directly to the objects stored in the bucket.

2. Volume Gateway (iSCSI) - This is for block based storage like OS, databases, virtual hardisk with VM. Volume interface presents applications with disk volumes using the iSCSI block protocol. Data written to volumes can be asynchronously backed up as point-in-time snapshots of volumes and stored in the cloud as Amazon EBS snapshots. Snapshots are incremental backups that capture only changed blocks. All snapshot storage is also compressed to minimize storage charges. Not for flat files though it is capable of handling flat files. It can be of type - Stored Volume and Cached Volume. Stored volume has all the data while cached volume only has the most frequently used items.

Stored Volume  - Lets you store your primary data locally, while asynchronously backing up that data to AWS. Stored volumes provide on-prem applications with low latency access to the entire datasets while providing durable, off-site backups. Storage volumes can also be created and mounted as iSCSI devices from on-prem application servers. DAta written to stored volumes is stored on on-prem storage hardware. This data is asynchronously backed up to S3 in the form of EBS snapshots. Stored volumes can be 1GB to 16TB in size.

Cached Volumes - Use S3 as primary data storage while retaining frequently access data locally on storage gateway. Cached volumes minimize the need to scale on-prem storage infrastructure while still providing applications with low latency access to frequently accessed data. Storage volumes can be upto 32TB in size and can be attached as iSCSI devices from on-prem application servers. 1GB - 32 TB is the size for cached volumes.

3. Tape Gateway (VTL) - Backup and archiving solution. Allows to create virtual tapes and send it to S3. Where lifecycle policies can be used to send it to glacier. Durable, cost effective solution. VTL interface allows to leverage existing tape-based backup applications. Each tape gateway is preconfigured with media changer and tape drives which are available to existing client backup applications as iSCSI devices.
