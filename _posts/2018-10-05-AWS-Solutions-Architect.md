---
layout: post
title: AWS Solutions Architect Overview
tags: AWS
---

I recently decided to get AWS Certified as a Cloud Solutions Architect - Associate.

[Blueprint for the Cloud Solutions Architect exam](https://aws.amazon.com/certification/certified-solutions-architect-associate/)

This post is an overview of the topics covered in the CSA - Associate certification.

## AWS Global Infrastructure 
22 Regions, 61 Availability zones and 96 edge locations.

Region - A region is a geographic zone. Each region has atleast 2 availability zones

Availability Zone - A datacenter. These are located in different parts of the same region such that natural disasters in one part of the region will not affect all availability zones at the same time.

Edge Locations - Edge Locations are endpoints for AWS which are used for caching content.

## Compute

### EC2
Virtual Machines inside AWS platform.

### EC2 Container Service
Run and manage docker containers

### Elastic beanstalk
Managed EC2 instances with auto configuration of scaling groups, RDS instances and deployment packages.

### Lambda
Serverless solution which can execute code when certain conditions are met. No OS/Virtual Machine management, organisation or other overhead required.

### Lightsail
Virtual Private Service for users who want to do minimal configuration. Still based on EC2 but most components are abstracted away for ease of use.

### Batch
Batch Computing in the cloud. Not covered by any certification 

## Storage

### S3
Object based storage. S3 is divided into buckets where all the files are stored.

### Elastic File Storage
Network attached storage. Files can be stored on EFS and mounted on multiple virtual machines.

### Glacier
Data archival. For data that doesnt change very often. Very very cheap

### Snowball
A storage device to bring in large amount of data into AWS. Data of the order of terabytes are easier to move by physically writing to a Snowball device and send it to AWS rather than send it over the internet.

### Storage Gateway
Virtual machines that can be installed in on-prem datacenters. They can replicate the information back on S3.

## Databases

### RDS
Relational databases like Aurora, MySQL, Oracle etc

### DynamoDB
Non-relational database

### Elasticache
Caching datastore

### Redshift
Data Warehousing or Business Intelligence service for complex queries.

## Migration

### AWS Migration Hub
Tracking service which allows to track applications as they are migrated into AWS and integrates with other services

### Application Discovery service
Detects the applications you have and their dependencies.

### Database Migration Service
Very easy way to migrate databases from on-prem to AWS

### Server Migration Service
Migrates servers from on-prem to AWS

### Snowball

## Networking

### VPC
Virtual Data center to configure firewalls, availability zones, network address ranges, network ACLs etc. To pass any associate certification you should under VPC inside-out and build one from memory

### CloudFront
Content Delivery Network. Can cache media files for users in different locations.

### Route53
DNS Server

### API Gateway
Create and secure APIs

### DirectConnect
Way of running dedicated line from your datacenter to Amazon. Connects directly to VPC. Important topic for CSA - Associate.

## Developer Tools - Not important for CSA-A

### CodeStar
Project Managing your code. 

### CodeCommit
Repositories/Source Control

### CodeBuild
Compile and run tests on your code. Produces software package ready to deploy

### CodeDeploy
Automates code deployments

### CodePipeline
Continous Delivery service

### X-Ray
Request tracing and performance monitoring tools for applications

### Cloud9
IDE environment to develop code

## Management Tools

### CloudWatch
Cloud Monitoring Service. Very important for Sysops Administrator Certification

### CloudFormation
Way of scripting infrastructure

### CloudTrail
Cloudtrail logs changed to AWS environments. 

### AWSConfig
Monitors configuration of AWS environments.

### OpsWorks
Similar to elasticbeanstalk. Uses chef and puppet to automate configuration of environments.

### Service Catalog
Manage a catalog of IT services that are approved to use on AWS. Not covered in exams.

### Systems Manager
An interface to manage AWS resources. 

### TrustedAdvisor
Gives advice across multiple domains like security or cost optimization etc. A virtual accountant for AWS

### Managed Service
Infrastructure Operations Management for AWS

## Media Services
Not covered in any exams

### Elastic Transcoder
Transcodes media to different formats

### MediaConvert 
File based media transcoding service

### MediaLive
Creates high quality videos

### MediaPackage
Packages and protects videos for delivery over the internet

### MediaStore
Storage service optimized for media

### MediaTailor
Targeted advertising into video streams 

## Machine Learning

### SageMaker
Deeplearning for developers

### Amazon Comprehend
Sentiment analaysis around data

### DeepLens
Artificially aware cameras. Physical camera.

### Lex
Powers Amazon Alexa Service. Way of communicating with customers.

### Machine Learning
Normal machine learning service. 

### Polly
Turns text into speech

### Rekognition
Recognises items in picture and video

### Amazon Translate
Translates different languages

### Amazon Transcribe
Turns speech into text

## Analytics

### Athena
Runs SQL queries against S3 buckets

### ElasticMapReduce
Used for processing large amounts of data

### CloudSearch/ElasticSearch
Search services 

### Kinesis
Ingesting large amounts of data into AWS, social media data etc

### Kinesis Video Streams
Specialised video version of Kinesis

### Quicksight
Business Intelligence tool. Not in any exams yet

### DataPipeline
Way to move data between different AWS services

### Glue
Used for Extract Transform Load. Not in any exams yet

## Security, Identity and Compliance

### Identity Access Management
Need to know inside out. Create user groups and access rules for each group.

### Cognito
Device authentication using third party providers

### GuardDuty
Monitors for malicious activity on AWS account. Not featured in exams

### Inspector
Agent that can be installed on EC2 which can monitor for security vulnerabilities.

### Macie
Scan S3 buckets and look for personally identifiable information

### Certificate Manager
Free SSL certificates if domain is registered through Route53

### CloudHSM
Hardware security module  - Used to store cases to access EC2 instances. Can be used to store encryption keys

### Directory Services
Integrate Microsoft Active Directory

### Web Application Firewall
Stops things like SQL injection, XSS attacks on application layer

### Shield
DDos mitigation and protection

### Artifact
On demand access to AWS compliance reports

## Mobile Services

### Mobile Hub
Helps to setup AWS services for mobile. Not included in any exams.

### AWS Pinpoint
Targeted push notifications to drive mobile engagement

### AppSync
Automatically updates data in web and mobile applications in realtime. Not included in exams.

### Device Farm
Test mobile apps on real live devices. Not included in exams

### Mobile Analytics
Analytics services for mobiles. Not included in exams.

## AR/VR

### Sumerian
Virtual Reality service to build VR environments. Still in preview.

## Application Integration

### Step Functions
Way to organise lambda functions to go through different steps. Not in exams.

### AmazonMQ
Messaging queue service based on RabbitMQ. Not in exams.

### SNS
Notification Service. Can be used to setup notification alarms

### SQS
Decouple infrastructure using a queue service

### Simple Workflow service
Used to process workflows

## Customer Engagement

### Connect
Call center in the cloud. Not in exams

### Simple Email Service
Way to send large number of emails. 

## Business Productivity

### Alexa for business
Use it like Siri :)

### Amazon Chime
Video conferencing for business

### Work Docs
Dropbox for AWS

### Workmail
Email from Amazon

## Desktop and App Streaming

### Workspaces
Run OS inside Amazon and stream down to device. Not in exams

### Appstream2.0
Stream the actual application to device. Not in exams

## IoT

### IoT Device Management
Streaming data from millions of devices

### Free RTOS
Operating System for Microcontrollers. Not in exams.

### Greengrass
Software that lets you run local compute messaging, data caching, sync and machine learning capabilities for connected devices. Not in exams.

## Game Development

### GameLift
Game Development platform. Not in exams.

## What you actually need for the Cloud Solutions Architect exam

1. Compute
2. Storage
3. Database
4. Migration
5. Network and Content Delivery
6. Management Tools
7. Security, Identity and Compliance
8. Analytics
9. Application Integration
10. Desktop and App Streaming

## What you actually need for the Cloud Solutions Architect exam

1. Compute
2. Storage
3. Database
4. Network and Content Delivery
5. Management Tools
6. Security, Identity and Compliance
7. Analytics
8. Application Integration