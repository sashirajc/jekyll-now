---
layout: post
title: Architecting for the cloud
tags: AWS
---

## Best Practices

Whitepapers

1. [AWS Architecting for the Cloud: Best Practices](../resources/AWS_CBP.pdf)

2. [AWS Well Architected Framework](../resources/AWS_WAF.pdf)

#### Business benefits of cloud

1. Almost zero upfront infrastructure investment

2. Just-in-time infrastructure

3. More efficient resource utilization

4. Usage-based costing

5. Reduced time to market

#### Technical benefits of cloud

1. Automation - "Scriptable infrastructure"

2. Autoscaling

3. Proactive Scaling

4. More efficient development lifecycle (CI/CD)

5. Improved Testability (Testing and development environments which are completely separate)

6. Disaster Recovery and Business Continuity

7. "Overflow" traffic to the cloud (Cloud can enhance on-prem resources)

#### Design for failure

Rule of thumb: Be a pessimist when designing architectures in the cloud; assume things will fail.  Assume hardware will fail. Assume outages will occue. Assume some disaster will strike your application. Assume that you will be slammed with more than the expected number of requests per second. ASsume that with time your application software will fail too. Always design, implement and deploy for automated recovery from failure. By being pessimistic, a better recovery strategy is devised right from design time, which helps in designing an overall system better.

#### Decouple Components

Build components that do not have tight dependencies on each other, so if one component dies or is busy, the other components in the system are built so as to continue to work as if no failure is happening.

Loose coupling isolates the various layers and components of the application so each component interacts asynchronously with others and treat them as 'black box'.

#### Implement Elasticity

1. Proactive Cyclic Scaling: Periodic scaling that occurs at fixed interval (daily, weekly, monthly, quarterly)

2. Proactive Event Scaling: Scaling just when you are expecting a big surge of traffic requests based on a scheduled business event such as product launches, marketing campaigns etc.

3. Autoscaling based on demand: Use a monitoring service, your system can send triggers to take appropriate actions so that it scales up or down based on metrics such as CPU utilization, network io etc

## Well Architected Framework

The well architected framework is a set of questions that can be used to evaluate how well your architecture is aligned to AWS best practices.

#### General Design Principles

1. Stop guessing capacity needs - Scale as and when it is needed.

2. Test systems at production scale - Use Cloudformation to replicate production environment in a test setting

3. Automate to make architectural experimentation easier - Use Cloudformation

4. Allow for evolutionary architectures - Business changes continously and architecture should have the provision to change and update (since this is easier to do on the cloud).

5. Data-Driven architecture - Log everything on Cloudwatch to see how the architecture impacts performance and remove bottlenecks in architecture.

6. Improve through game days - Simulate events like new year sale in a test environment to prepare production environment better

### Pillar 1: Security

#### Design Principles

1. Always apply security at all layers (Not just on firewall level) - Security should be on subnets, firewalls, security groups, ACLs and on the instances themselves.

2. Enable traceability - If a hacker or malicious actor is in the picture, all their actions should be traceable.

3. Automate responses to security events - If someone is trying to brute force SSH then it should trigger a SNS notification.

4. Focus on securing the system - Secure data, application and operating system

5. Automate security best practices - Use Center for Internet Security as a guide on how to harden operating systems and create an AMI. Use this AMI with security settings for all EC2 instances.

6. Shared security model - Customer is responsible for IAM access policies, firewall config, instance hardening, server side and client side encryption etc.

AWS will be responsible for data center security, applying software patches to cloud resources and maintaining availability and reliability of the resources as per the SLAs.

#### Definition

Security in the cloud consists of 4 areas:

1. Data Protection: Basic data classification should be in place. Data should be organised and classified into segments such as publicly available, available only to members of organisation, available only to certain members of the organisation, available only to the board etc.

Least privilege access system must be implemented so that people are only able to access what they need. All data must be encrypted whenever possible, in transit or at rest.

2. Privilege Management

Privilege management ensures that only authorized and authenticated users are able to access your resources and only in a manner that is intended. It can include using Access Control Lists, Role based access controls and password management.

3. Infrastructure Protection

Outside of Cloud, how would you protect your data center? RFID controls, security cameras, lockable cabinets etc. Within AWS they handle this, so really infrastructure protection exists at a VPC level. How are you managing ACLs? How is the routing done? Are the subnets public or private?

4. Detective Controls

Detective controls can be used to detect or identify a security breach. AWS services to achieve this include - CloudTrail, CloudWatch, Config, S3, Glacier

#### Best Practices

1. Data Protection

..* AWS customers maintain full control over their data.

..* AWS makes it easier to encrypt data and manage keys, including key rotation which can be easily automated natively by AWS or maintained by the customer.

..* Detailed logging is available that contains important content such as file access and changes.

..* AWS has designed storage systems for exceptional resilience.

..* Versioning, which can be a part of a larger data lifecycle management process, can protect against accidental overwrites, deletes and similar harm.

..* AWS never initiates the movement of data between regions. Content placed in a region will remain in that region unless customer explicitly enables a features or leverages a service that provides that functionality.

#### Questions to ask

1. Data Protection

..* How are you encrypting and protecting data at rest?

..* How are you encrypting and protecting data in transit?

2. Privilege Management

..* How are you protecting access to and use of the AWS root account credentials?

..* How are you defining roles and responsibilities of system users to control human access to the AWS management console and APIs?

..* How are you limiting automated access to AWS resources?

..* How are you managing keys and credentials?

3. Infrastructure protection

..* How are you enforcing network and host-level boundary protection?

..* How are you securing access to subnets?

..* How are you securing access to accounts on EC2 instance? Is it just the ec2-user account or are there multiple accounts?

..* Are you using bastian hosts or NAT Gateway?

..* How are you enforcing AWS level protection? Are there multiple users with console level access? Are there multi-factor authentication enabled for all the users? Do you have strong password protection policies?

..* How are you protecting the integrity of the operating system? Are windows instances getting anti-virus updates? Are the operating systems hardened?

4. Detective Control

..* How are you capturing and analyzing AWS logs?

..* Do you have cloudtrail turned on, in each region?

..* Are you using a log management plans?

#### Key AWS Services

1. Data Protection - ELB, EBS, S3, RDS

2. Privilege Management - IAM, MFA

3. Infrastructure protection - VPC

4. Detective Control - CloudTrail, CloudWatch, Config

### Pillar 2: Reliability

Reliability covers the ability of a system to recover from service or infrastructure outages/ disruptions as well as the ability to dynamically acquire computing resources to meet demand.

#### Design Principles

1. Test recovery procedures - Introduce failure into the environment and test how the the system recovers

2. Automatically recover from failure - Use KPIs to notify when performance thresholds are breached. This allows for automatic reovery from failures.

3. Scale horizontally to increase aggregate system availability - Scale out rather than scale up, this can ensure one system does not become a block point.

4. Stop guessing capacity - Use autoscaling to meet demand as needed instead of underprovisioning or over provisioning.

#### Definition

1. Foundations - AWS takes care of most of the foundational limits. However there are service limits on AWS to ensure that customers do not overprovision resources. Most services have a service limit which can be extended by contacting customer support.

2. Change management - You need to be aware of how change affects a system so that you can plan proactively around it. Monitoring allows you to detect any changes to the environment and react. Cloudwatch can be used to monitor the environment and services such as autoscaling to automate change in response to changes on production environment.

3. Failure Management - With cloud, you should always architect your systems with the assumptions that failure will occue. You should become aware of these failures, how they occured, how to respond to them and then plan on how to prevent these from happening again.

#### Best Practices

1. Foundations - 

..* How are you managing AWS service limits for your account?

..* Are you aware of the service limits on AWS?

..* How are you planning your network topology on AWS?

..* Do you have an escalation path to address issues?

2. Change management - 

..* How does your system adapt to changes in demand?

..* How are you monitoring AWS resources?

..* How are you executing change management?

3. Failure Management - 

..* How are you backing up your data?

..* How does your system withstand component failures?

..* How are you planning for recovery?

#### Key AWS Services

1. Foundations - IAM, VPC
2. Change Management - CloudTrail
3. Failure Management - CloudFormation

### Pillar 3: Performance Efficiency


#### Design Principles


#### Definition


#### Best Practices


#### Key AWS Services


#### Resources


### Pillar 4: Cost Optimization


#### Design Principles


#### Definition


#### Best Practices


#### Key AWS Services


#### Resources


### Pillar 5: Operational Excellence


#### Design Principles


#### Definition


#### Best Practices


#### Key AWS Services


#### Resources

