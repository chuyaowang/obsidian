# Cloud Essentials

> [Source](https://explore.skillbuilder.aws/learn/course/134/play/85854/aws-cloud-practitioner-essentials)

## Module 1

> [!summary] Client-Server Model
> 
> In computing, a **client** can be a web browser or desktop application that a person interacts with to make requests to computer servers. A **server** can be services, such as Amazon Elastic Compute Cloud (Amazon EC2) – a type of virtual server.

> [Whitepaper: Overview of AWS](https://d0.awsstatic.com/whitepapers/aws-overview.pdf)

> [!summary] Cloud Computing
> 
> On-demand delivery of IT resources and applications through the internet with [pay-as-you-go](#^payasyougo) pricing.

> [!note] Pay-as-you-go
> 
> Pay for the amount of resources used, and stop using and paying when the resources are not needed. AWS allows for rapidly obtaining and releasing computing resources.
^payasyougo

> [!info] 3 Types of Deployment
> 
> - Cloud-based: all parts of the app run on the cloud.
> - On-premise: also know as *private cloud*. Run apps on local data centers, and use virtualization and application management tools to increase resource efficiency.
> - Hybrid: data analysis in cloud and app kept local. Or other ways to run the app part in cloud and part local.

## Module 2

### Introduction

> [!summary] Multitenancy
> 
> Multiple virtual machines sharing a physical machine.

```ad-summary
title: Tenancy

How instances are distributed on the hardware:
- Shared: multiple instances sharing the hardware
- Dedicated Instance: one instance per hardware;
- Dedicated Host: a physical server dedicated just for you, multiple instances can be placed on this server.

```
^tenancy

> [!summary] Hypervisor
> 
> The program that manages virtual machines and allocate resources.

> [!note] EC2
> 
> Elastc compute cloud (EC2) is a service that is used to access the virtual servers provided by AWS. The 2 signifies 2 Cs in the name.
> 
> EC2 is run as *instances*. The system and software installed on EC2 can all be configured. The CPU, RAM, and storage available can also be scaled easily.

> [!info] Advantages of Using EC2
> 
> - You can provision and launch an Amazon EC2 instance within minutes.
> - You can stop using it when you have finished running a workload.
> - You pay only for the compute time you use when an instance is running, not when it is stopped or terminated.
> - You can save costs by paying only for server capacity that you need or want.

### EC2 Instance Types

> [!tip]
> 
Also known as EC2 instance families

> [!note] General Purpose
> 
> - Balanced computing, memory, and storage resources.
> - Good for app servers, web servers, game servers, backend servers, and small and medium databases.

> [!note] Compute Optimized
> 
> - Higher computational power.
> - Suitable for compute-intensive app, game, web servers, and scientific modeling.
> - Also can be used for batch processing workloads that require [processing many transactions in a single group](Batch%20Processing.md).


> [!note] Memory Optimized
> 
> - Provides high memory.
> - Ideal for high-performance *database *or a workload that involves performing real-time processing of a large amount of unstructured data.

> [!note] Accelerated Computing
> 
> - Uses [hardware accelerators or coprocessors](Coprocessors.md).
> - Hardware accelerators perform better in floating point number calculations, graphics processing, and data pattern matching.
> - Good for graphics applications, game streaming, and application streaming.

> [!note] Storage Optimized
> 
> - Designed for workloads that require high, sequential read and write access to large datasets on local storage.
> - Examples: distributed *file* systems, data warehousing applications, and high-frequency online transaction processing (OLTP) systems
> - High input/output operations per second (IOPS) capacity.

### Pricing

> [!summary] Availability Zone & Region
> 
An availability region is a large geographic region containing the AWS servers. Each region consists of multiple zones. Zones are isolated from other zones' failures.
^avail

> [!note] On-Demand
> 
> **On-Demand Instances** are ideal for short-term, irregular workloads that cannot be interrupted. No upfront costs or minimum contracts apply. The instances run continuously until you stop them, and you pay for only the compute time you use.
> 
> Suited for short or unpredictable usage, such as in a development environment.

> [!note] Reserved
> 
> State upfront what *instance type and size* (like M5.large), *platform*, and *[tenancy](#^tenancy)* to use in one region, and make a 1 or 3 year commitment. For the **standard reserved instances**, also have the option to specify an availability *zone* for the reserved instance, known as **capacity reservation**. 
> 
> For **convertible reserved instances**, the availability zone and instance type can change, but the discount is lower.
> 
>  Suited for steady state, long-term usage. When the commitment period ends, on-demand rates apply. Either terminate the instance or start a new one.

> [!note] Saving Plan
> Another discount plan that gives discount from the on-demand rates. The user makes a *dollars spent per hour* commitment for 1 to 3 years. Usage up to the commitment is charged at the **saving plan** rates. Above the rate, on-demand rates apply. 
> 
> Any usage of an EC2 instance in a *chosen region* can enjoy the reduced cost. The plan does not require instance type and size, OS, and tenancy to be specified get a discount. Also do not need to commit a certain number of instances for 1 or 3 years. The plan does not have an EC2 capacity reservation option. 
> 
> Suitable for more flexible, long-term usage.

> [!note] Spot Instances
> The highest discount, up to 90%. The **spot instance** can be started when there is capacity, and when the capacity is scarce or requests for spot instances increase, the spot instance will be interrupted. 
>
> Suitable for workloads that can withstand interruptions.

> [!note] Dedicated Host
> **Dedicated Hosts** are physical servers with Amazon EC2 instance capacity that is fully dedicated to your use. 
> 
> You can use your existing per-socket, per-core, or per-VM software licenses to help maintain license compliance. You can purchase On-Demand Dedicated Hosts and Dedicated Hosts Reservations. Of all the Amazon EC2 options that were covered, Dedicated Hosts are the most expensive.













