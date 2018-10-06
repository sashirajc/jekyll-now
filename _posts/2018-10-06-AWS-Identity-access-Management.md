---
layout: post
title: AWS Identity Access Management (IAM)
tags: AWS
---

IAM allows to manage users and their level of access to the AWS console.

IAM is universal. It does not apply to specific regions.

Root account is the account used to setup the AWS account. It has complete Admin access.

### IAM gives:
1. Centralised control of AWS account
2. Shared access to AWS account
3. Granular Permissions for each user
4. Identity Federation (login from Active Directory, Facebook, LinkedIn etc)
5. Multifactor Authentication
6. Provide temporary access for users/devices and services where necessary
7. Allows you to setup your own password rotation policy
8. Integrates many different AWS services
9. Supports PCI DSS Compliance

### Critical Terms
1. Users - End Users
2. Groups - Collection of users with same set of permissions
3. Roles - Permissions assigned to AWS resources. Like EC2 instance being given the permission to write to S3 etc
4. Policy - Group of rules that define one of more permissions. Policies can be applied to users/groups or roles.

### Notes

New users are created with no permissions. All permissions must be explicitly added to each user/user group.

Two types of access - 
1. Programmatic access: Grants access to AWS resources via CLI. Credentials needed are Access Key ID and Secret access key
2. Console access: Grants access to the AWS console and dashboard. Credentials needed are username and password.

Programmatic access and console access are not interchangeable.

Credentials are only given once. If lost, they have to be regenerated. There is an option to download and save those in a local secure location.

Policies can be created for each user to give them access to specific resources and permissions on how the resources are used. Policies are JSON documents which can be edited.

Users can get access policies individually as well as from the user groups that they belong to.

Roles - Secure way to grant permissions to entities that you trust.
Examples - 
1. IAM user in another account
2. Application code running on an EC2 instance that needs to perform actions on AWS resources like reading/writing from database.
3. An AWS service that needs to act on resources in your account to provide its feature

Billing alarms can be created to monitor the bill. When the bill exceeds the set threshold AWS would send an email to alert us.