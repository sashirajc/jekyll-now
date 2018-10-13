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


#### Definition


#### Best Practices


#### Key AWS Services


#### Resources

### Pillar 2: Reliability

#### Design Principles


#### Definition


#### Best Practices


#### Key AWS Services


#### Resources



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

