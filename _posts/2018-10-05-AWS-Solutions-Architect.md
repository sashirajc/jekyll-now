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

##  Networking

### VPC
Virtual Data center to configure firewalls, availability zones, network address ranges, network ACLs etc. To pass any associate certification you should under VPC inside-out and build one from memory

### 