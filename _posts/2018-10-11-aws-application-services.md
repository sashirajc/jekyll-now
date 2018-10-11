---
layout: post
title: AWS Application Services
tags: AWS
---

## Simple Queue Service

First ever AWS service

SQS is a web service that gives access to a message queue that can be used to store messages while waiting for a computer to process them.

SQS can be used to decouple the components of an application so they can run independently, easing message management between components.

Any component of a distributed application can store messages in the queue. Messages can contain upto 256kB of text in any format. Any component can later retrieve the messages programatically using the SQS API.

The queue acts as a buffer between the component producing and saving the data, and the component receiving the data for processing. This overcomes any network issues between the producer and the consumer and also prevents the producer from being overloaded.

An autoscaling group can be configured to check the number of messages waiting in SQS to be processed and can kick off a new EC2 instance if there are too many messages waiting to be processed.

SQS is pull based, not push based. An EC2 instance or something must constantly poll looking for new messages.

Messages are 256KB in size

They can be kept in the queue from 1 minute to 14 days.

Default retention period is 4 days.

Visibility Timeout
The amount of time that the message is invisible in the SQS queue after a reader picks up that message. If the job is processed before the visibility timeout expires, the message will then be deleted from the queue. If the job is not processed within that time, the message will become visisible again and another reader will process it. Default visibility timeout is 30 seconds. Maximum is 12 hours.

Long Polling

Long polling is a way to retrieve messages from SQS queues, it doesnt return a response until a message arrives in the message queue. This can save quite a bit of money.

Queue Types
1. Standard Queues

Default queue type. Unlimited number of transactions per second. Guarantee that a message is delivered atleast once. Ocassionally more than one copy of the message might be delivered out of order. Standard queues provide best effort ordering which ensures that messages are generally delivered in the same order as they are sent.

2. FIFO Queues

They will be processed in the same order they are sent. Message is delivered only once and remains available until a consumer processes and deletes it. Duplicates are not introduced into the queue. 

FIFO queues also support message groups that allow multiple ordered message groups within a single queue. FIFO queues are limited to 300 transactions per second, but have all the capabilities of standard queues.

## Simple Workflow Service

Web service that makes it easy to coordinate work across distributed application components. SWF enables applications for a range of use cases, including media processing, web application backends, business process workflows and analytics pipelines to be designed as a coordination of tasks.

Tasks represent invocations of various processing steps in an application which can be performed by executable code, web service calls, human actions and scripts.

SWF Workers

Programs that interact with SWF to get tasks, process received tasks and return results.

SWF Decider

Program that controls the coordination of tasks, ordering, concurrency and scheduling according to the application logic.

Workers and decider can run on EC2 and on machines behind firewalls. SWF brokers interactions between the decider and workers. Allows decider to get consistent views into the progress of tasks and initiate new tasks in an ongoing manner.

SWF stores tasks, assigns them to workers when they are ready and monitors their progress. Ensures that a task is assigned only once and is never duplicated. SWF maintains the application's state durable, workers and deciders dont have to keep track of execution state. They can run independently and scale quickly.

Workflow and activity types and workflow execution are scoped into a domain. Domains isolate a set of types, executions and task lists from others within the same account. Domains can be registered from the console or by using the RegisterDomain API.

Maximum workflow can be 1 year and value is measured in seconds.

SWF presents a task oriented API whereas SQS offers a message oriented API

SWF ensures that a task is assigned only once and is never duplicated. SQS handle duplicated messages and may ensure that a message is processed only once.

SWF keeps track of all tasks and events in an application. With SQS, we need to implement our own application-level tracking especially if application uses multiple queues.

## Simple Notification Service

Web service that makes it easy to setup, operate and send notifications from the cloud. Provides capability to publish messages from an application and immediately deliver them to subscribers or other applications.

Push notifications to Apple, Google, FireOS and Windows devices.

SNS can also deliver notifications by SMS, email, SQS queues or to any HTTP API. Lambda functions can also be triggered with SNS notifications. The payload of the published message will be the input parameter for Lambda function and can manipulate the information in the message, publish the message to other SNS topics or send the message to other AWS services.

SNS allows to group multiple recipients using topics. A topic is an access point for allowing recipients to dynamically subscribe for identical copies of the same notification. One topic can support deliveries to multiple endpoint types. When you publish once to a topic, SNS delivers appropriately formatted copies of the message to each subscriber.

All messages are stored reliable under multiple az

Benefits

1. Instantaneous, push based delivery.
2. Simple APIs and easy integration with applications
3. Flexible message delivery over multiple transport protocols
4. Inexpensive, pay-as-you-go model
5. Web based Console offers simplicity to use

## Elastic Transcoder

Media transcoder in the cloud. Convert media files from original source format to different formats.

Pay based on the minutes that you transcode and resolution you transcode.

## API Gateway

Fully managed service that makes it easy for developers to publish, maintain, monitore and secure APIs at any scale. 

API Caching

API Gateway can cache endpoint's response. With caching, the number of calls made to the endpoint can be reduced and also latency of the requests to the API can be improved. Caching can also have a TTL for which the API response can be cached.

API gateway can also throttle requests to prevent attacks.

Same origin policy - A web browser permits scripts contained in a first web page to access data in a second web page, but only if both web pages have the same origin.

Cross-Origin Resource Sharing

CORS is one way the server at the other end can relax the same-origin policy.

CORS is a mechanism that allows restricted resources on a webpage to request from another domain outside the domain from which the first resource was served.

## Kinesis

Kinesis is a AWS platform to send streaming data. Kinesis makes it easy to load and analyze streaming data and also provide the ability to build your own custom applications according to business needs.

Streaming Data

Data that is generated continously by thousands of data sources, which typically send in the data records simultaneously and in small sizes.

Kinesis Streams

Data producers can produce data and send it  to Kinesis streams. 

They are stored on shards on the Kinesis stream for upto 7 days (normally 24 hours).

Consumers can be run on the shard to perform operations/calculations. Once they finish they can send the data over to datastores.

Multiple shards can be on a stream. 

Kinesis Firehouse

Dont have to worry about shards,streams or consumers. These are all automated and analyzed without intervention.

Kinesis Analytics

Way to run SQL queries.

