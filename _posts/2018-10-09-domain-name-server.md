---
layout: post
title: Domain Name Server (DNS)
tags: AWS
---

DNS is used to convert  a domain name into an IP address. Internet Protocol (IP) address are of IPv4 and IPv6 types

IPv4 - 32 bit field with 4 billion addresses

IPv4 - 128 bits, 340 undecillion addresses

Top Level domains name- Last word in a domain name is the top level domain - .com,.edu,.uk,.sg

Second Level domain name - The second word in domain name.

Top level domains are controlled by Internet Assigned Numbers Authority (IANA)

Domain Register - All domain names inside a top level domain needs to be unique. Domain registers are the authority that can assign domain names directly under top level domains. These domains are registered with InterNIC, a service of ICANN which enforces uniqueness of domain names across the internet. Each domain name is registered in a central database called WhoIs

DNS operates on port 53. Amazon Route53 gets its name from here.

Start of Authority Record
The record stores information about
1. The name of the server that supplied the data for the zone.
2. The administrator of the zone
3. The current version of the data file.
4. Default number of seconds for the time-to-live file on resource records.

TTL should be as small as possible so changes made can propagate faster

NS Records

NS stands for name server records. Top Level domain servers use NS to direct traffic to content DNS servers which contain the authoritative DNS records.

A Record 

Fundamental type of DNS record. A stands for 'address'. A record is used by the computer to translate domain name to IP address.

CNames

Canonical Name - Can be used to resolve one domain name to another.

Alias Record 

Alias records map resource record sets in hosted zone to other AWS resources that are configured as websites. CNames wont work with naked domain names (domain names without www). Alias record is specific to Route53 so they can use AWS resources which have naked domain names as Cnames.

Given a choice, choose alias names instead of cnames for the exam.

Alias records can save time because Route53 automatically recognises changes in the record sets that the alias resource record set refers to. If the public IP address of a load balanacer changes, Route53 will automatically reflect those changes in the DNS records without any changes to the hosted zone that contains the resource record sets.

## Simple Routing

Only one record with multiple IP addresses. If multiple values are specified in a record, Route53 returns all values to the user in a random order.

## Weighted Routing

Split traffic based on weighted percentage. Allows to specify what percentage of traffic should go to a certain IP address. 20% can be diverted to US-EAST-1 and 80% can be sent to US-WEST-1

## Latency

Latency based routing allows to route traffic based on lowest network latency for the end user.

## Failover

Creates an active/passive setup. With active or primary webserver in one region and the secondary site in another region. Route53 monitors the health of the primary site with a healthcheck. If the healthcheck fails on the primary, the secondary site would take over.

