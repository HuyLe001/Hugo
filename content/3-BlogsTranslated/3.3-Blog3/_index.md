---
title: "Game Developer's Guide to Amazon DocumentDB Serverless"
date: "2025-09-11"
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

{{% notice warning %}}
 **Note:** The information below is for reference purposes only. Please **do not copy verbatim** for your report, including this warning.
{{% /notice %}}

# GAME DEVELOPER'S GUIDE TO AMAZON DOCUMENTDB SERVERLESS

**Original Article:** [Game developer's guide to Amazon DocumentDB Serverless](https://aws.amazon.com/vi/blogs/gametech/game-developers-guide-to-amazon-documentdb-serverless/)

**Original Authors:** Jackie Jiang, Douglas Bonser, and Matthew Nimmo

**Publication Date:** 18 NOV 2025

---

Today, we'll explore how Amazon DocumentDB Serverless helps game developers streamline operations, handle unpredictable traffic, and optimize cost.

---

## WHAT IS AMAZON DOCUMENTDB SERVERLESS

Amazon DocumentDB Serverless is an on-demand, auto scaling configuration for Amazon DocumentDB (with MongoDB compatibility). It automatically scales capacity up or down in fine-grained increments based on your application's demand. It eliminates the need to manually provision, scale, and manage database instances while verifying you only pay for the resources you actually consume.

---

## WHY GAME STUDIOS SHOULD CARE

For game studios managing player data, leaderboards, and game state, database management can be a significant operational headache. Amazon DocumentDB Serverless offers a compelling solution that's particularly well-suited for the dynamic workloads common in gaming applications.

- **Launch day flexibility:** There is no more guessing about what instance size is needed for launch day. Amazon DocumentDB Serverless automatically scales up to handle player surges, then scales down during quiet periods.
- **Cost optimization:** For seasonal games or those with distinct peak hours, you're only paying for actual usage. When your European players are sleeping and your US players haven't logged in yet, you're not burning money on idle database capacity.
- **Development environment efficiency:** Testing new features or running QA environments? Amazon DocumentDB Serverless is perfect for development workloads where database usage is sporadic, but high performance is still crucial.

---

## REAL GAMING SCENARIOS

Following are some gaming scenarios where Amazon DocumentDB Serverless could be of assistance:

### Live service games

- **Example:** During a season finale event in a battle royale game, player counts might spike from 50,000 to 500,000 in minutes. Amazon DocumentDB Serverless automatically scales to handle millions of concurrent inventory checks and match result writes.
- **Daily reset management:** When all players simultaneously claim daily rewards at reset time, the database seamlessly handles the surge without pre-provisioning.
- **Special events:** During a rare item drop event, the database can handle thousands of simultaneous inventory updates and marketplace transactions.

### Cross-platform MMOs

- **Example:** An MMO launches a new raid boss at different times across regions. As Asian servers peak, then European, then American, the database capacity follows the wave of player activity around the globe.
- **Guild system data:** Manages complex guild hierarchies, permissions, and shared inventories that require frequent updates and reads.
- **Trading systems:** Handles auction house transactions and player-to-player trading with consistent performance regardless of market activity.

### Mobile games with unpredictable growth

- **Example:** A casual mobile game suddenly goes viral on TikTok, growing from 10,000 to 1,000,000 daily active users in 48 hours. Amazon DocumentDB Serverless adapts automatically without developer intervention.
- **Social features:** Manages friend lists, gifting systems, and social interactions that can spike during promotional events.
- **Season pass progress:** Tracks and updates millions of players' battle pass progress simultaneously.

---

## UNDERSTANDING AMAZON DOCUMENTDB CAPACITY UNITS

When a surge of players hits your game servers, Amazon DocumentDB Serverless automatically detects the increased load and scales compute power and memory. It measures usage in Amazon DocumentDB capacity units (DCUs). Each DCU is a combination of approximately 2 gibibytes (GiB) of memory, corresponding CPU, and networking.

Each Amazon DocumentDB Serverless writer, or reader, has their capacity measured in DCUs. It is represented as a floating-point number that adjusts up or down with scaling. This capacity is updated every second. We recommend setting the minimum capacity to enable each writer, or reader, to keep the application's working set in the buffer pool. This prevents the buffer's content from being discarded during idle times.

Before adding Amazon DocumentDB Serverless instances to a cluster, the cluster must have the ServerlessV2ScalingConfiguration parameter set. This parameter defines the serverless instance capacity range with two values, MinCapacity and MaxCapacity, with a capacity range of 0.5256 DCUs. During a major guild raid or tournament, your database might need 64 DCUs to handle the load. During off-peak hours, it might scale down to 0.5 DCUs.

Amazon DocumentDB Serverless continuously monitors CPU, memory, and network utilization (collectively called load) for each serverless writer or reader. This includes both application database operations, and background database and administrative tasks. When capacity limits are met or performance issues arise, Amazon DocumentDB Serverless automatically scales up to maintain optimal performance. Scaling increments start as small as 0.5 DCUs, with larger current capacities allowing bigger increments and faster scaling.

When Amazon DocumentDB Serverless writers or readers are idle, instances can scale down to an idle state of 0.5 DCUs if MinCapacity is set to 0.5. In this state the compute resources are insufficient for most production workloads, but the instances remain ready to quickly scale up. Upon exiting an idle state, instances scale directly to at least 1.02.5 DCUs (or the MaxCapacity, if lower). To enable scaling down to 0.5 DCUs, instance capacity is limited whenever MinCapacity is 1.0 DCUs or less.

The charges for Amazon DocumentDB Serverless capacity are measured in terms of DCU hours. By billing for each DCU usage, instead of maintaining high-capacity instances for peak times, serverless databases align their costs with actual player activity. This frees your development team to focus on building game features rather than forecasting and managing infrastructure.

---

## REQUIREMENTS AND CONSIDERATIONS

Amazon DocumentDB Serverless requires that clusters are running engine version 5.0.0, and it is not supported in older engine versions. While some Amazon DocumentDB features are compatible with Amazon DocumentDB Serverless, they may cause performance issues or out-of-memory errors if your capacity range is insufficient for your workload's memory requirements.

Features requiring higher MinCapacity or MaxCapacity settings include Performance Insights and serverless instance creation on clusters with large data volumes (including during cluster restoration). If you encounter Out-of-memory errors due to capacity misconfiguration read Avoiding out-of-memory errors for more information. Amazon DocumentDB Serverless instances do not support global clusters.

---

## MIGRATING TO SERVERLESS

Each Amazon DocumentDB cluster can use serverless capacity, provisioned capacity, or both in a mixed configuration. For example, combine a large, provisioned writer with serverless readers for higher write throughput, or use a serverless writer with provisioned readers when writes are variable, but reads are steady. It's also possible to configure a cluster to use only serverless, either by creating a new serverless cluster or converting existing provisioned capacity.

To migrate to Amazon DocumentDB Serverless, first upgrade the cluster to the supported engine version 5.0.0. Configure scaling by adding serverless instances and optionally perform a failover operation to make a serverless instance the cluster writer. You then optionally convert provisioned instances to serverless or remove them.

Migration from MongoDB requires Amazon Web Services (AWS) Database Migration Service (AWS DMS) for online, minimal-downtime migrations, or native MongoDB tools for offline dump and restore. Review Migrating to Amazon DocumentDB Serverless for detailed step-by-step guidance and best practices.

After migration, follow Amazon DocumentDB best practices by optimizing indexes, monitoring key performance metrics, enforcing security and cost controls. Be certain to tune your workloads to confirm reliability, efficiency, and scalability.

---

## MONITORING SERVERLESS USAGE

Amazon DocumentDB Serverless provides granular monitoring through Amazon CloudWatch metrics which update every second to give real-time insight into instance scaling and resource usage. Typically, most scaling up for Amazon DocumentDB Serverless instances is caused by memory usage and CPU activity. Alternatively, you can use Performance Insights to monitor the performance of Amazon DocumentDB Serverless instances.

Amazon DocumentDB Serverless offers four critical monitoring metrics to help you track performance and optimize resource allocation:

1. **ServerlessDatabaseCapacity:** Measures the current capacity of each instance in DCUs, reflecting CPU, memory, and networking resources. At the cluster level, it averages the capacity across all serverless instances.

2. **DCUUtilization:** Measures the percentage of current database capacity used relative to the maximum configured capacity. If it nears 100%, the instance has scaled to its limit, and users should consider increasing the max DCU or adding more reader instances to balance workloads.

3. **CPUUtilization:** Represents the percentage of CPU currently used relative to the CPU capacity available under the cluster's maximum DCU setting. It monitors CPU usage continuously and triggers automatic scaling when usage is consistently high.

4. **FreeableMemory:** Represents the amount of unused memory available when the instance is scaled to its maximum capacity, increasing by about 2 GiB for each DCU below the max capacity.

---

## SUMMARY

Amazon DocumentDB Serverless delivers streamlined elasticity that game developers need by eliminating pre-sizing guesswork, handling event surges, and aligning costs with existing player activity. By automatically scaling database capacity based on actual demand, Amazon DocumentDB Serverless provides game developers with a way to focus on creating engaging player experiences, while AWS handles the database infrastructure complexity.

Contact an AWS for Games specialist to know how we can help accelerate your business.

---

## FURTHER READING

- [Amazon DocumentDB Serverless is now available](https://aws.amazon.com/blogs/aws/amazon-documentdb-serverless-is-now-available/)
- [Using Amazon DocumentDB Serverless](https://docs.aws.amazon.com/documentdb/latest/developerguide/docdb-serverless.html)
- [JSON database solutions in AWS: Amazon DocumentDB (with MongoDB compatibility)](https://aws.amazon.com/blogs/database/json-database-solutions-in-aws-amazon-documentdb-with-mongodb-compatibility/)
- [Game Developer's Guide to Amazon DocumentDB Part 1: An Overview](https://aws.amazon.com/blogs/gametech/game-developers-guide-to-amazon-documentdb-part-1-an-overview/)
- [Choosing the scaling capacity range for a DocumentDB serverless cluster](https://docs.aws.amazon.com/documentdb/latest/developerguide/docdb-serverless-scaling-config.html#docdb-serverless-scaling-capacity-choosing)

---

## ABOUT THE AUTHORS

![Jackie Jiang](https://d2908q01vomqb2.cloudfront.net/91032ad7bbcb6cf72875e8e8207dcfba80173f7c/2024/07/24/Jackie-Jiang.png)

**Jackie Jiang** is a Principal Solutions Architect at AWS. Jackie works with enterprise gaming customers to support their innovation in the cloud. She leverages 20+ years of cross-industry experience to help her customers bring their visions to life in a reliable, scalable, and cost-effective manner.

![Douglas Bonser](https://d2908q01vomqb2.cloudfront.net/91032ad7bbcb6cf72875e8e8207dcfba80173f7c/2025/11/17/Douglas-Bonser.png)

**Douglas Bonser** is a Senior DocumentDB Specialist Solutions Architect. He brings 30+ years working extensively with NoSQL and relational database technologies. Douglas enjoys helping customers solve problems and modernize their applications using NoSQL database technology.

![Matthew Nimmo](https://d2908q01vomqb2.cloudfront.net/91032ad7bbcb6cf72875e8e8207dcfba80173f7c/2025/11/06/Matthew-Nimmo.png)

**Matthew Nimmo** is a Solutions Architect for Game Tech at AWS. As both a technologist and avid gamer, he helps game studios leverage cloud technology to solve complex challenges and create better player experiences.
