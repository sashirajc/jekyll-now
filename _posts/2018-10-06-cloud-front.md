---
layout: post
title: AWS Cloud Front
tags: AWS
---

A content delivery network (CDN) is a system of distributed servers that deliver webpages and other web content to a user based on the geographic location of the user, the origin of the webpage and a content delivery server.

Edge location - This is the location where the content will be cached. There are more edge locations than AWS regions or availability zones.

Origin - The origin of all files that the CDN will distribute. This can be either an S3 bucket, an EC2 instance or an elastic load balancer.

Distribution - This is the name given to the CDN which consists of a collection of edge locations.

* Web Distribution - Used for websites
* RTMP - Used for Media Streaming

Amazon Cloudfront can be used to deliver the entire website, including dynamic, static, streaming and interactive content using a global network of edge locations. Requests for content are automatically routed to the nearest edge locations to give the best performance.

Amazon Cloudfront can work seamlessly with both AWS resources and non-AWS origin sources.

Edge locations can also be written to. Objects are cached for life of the TTL.The typical TTL is 24 days.

Cached objects can also be cleared for a small price. 

Each distribution can have multiple origins.

Cloudfront can whitelist or blacklist countries where cloudfront can be allowed to distribute content.

