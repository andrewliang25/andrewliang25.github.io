---
title: 'Distributed Transactions, CAP Theorem, ACID, and BASE'
date: 2024-02-19 17:41:29
tags:
---


## What is a transaction and why distributed?

A transaction is a sequence of operations that are performed as a single unit of work. The main goal of a transaction is to ensure that the data remains consistent and reliable, even in the face of failures or errors.

Achieving scalability and availability requires distributed systems. Also, to guarantee atomicity in global transactions across components.

There are two kinds of structures in distributed transactions:

{% asset_img Flat-Nested-TX.png Flat and Nested Transactions %}


<!-- more -->

## CAP Theorem

{% asset_img CAP_Theorem_Venn_Diagram.png CAP Theorem %}

+ Consistency(Strong): Every read receives the most recent write or an error.
+ Availability: Every request receives a (non-error) response, without the guarantee that it contains the most recent write.
+ Partition Tolerance: The system continues to operate despite an arbitrary number of messages being dropped (or delayed) by the network between nodes.

CAP theorem states that any distributed data store can provide only two of the above three guarantees.

Therefore, there are 3 options for building a system:
1. CA: Monolithic system. Most centralized RDBMS have these properties.
2. CP: System returns error before all nodes have synchronized to latest update. Some distributed RDBMS(clustering) use this practice.
3. AP: DNS and some NoSQL database implement this practice. These systems have high availability but may not return the latest data.

Before CAP has been released, there are two terms you still need to know: ACID and BASE.

## ACID

In RDBMS, if transactions satisfy following properties, they are considered safe and valid:

+ Atomicity: All actions in a transaction either succeeds completely or fails completely.
+ Consistency: A transaction can only bring the database from one consistent state to another, preserving database invariants
+ Isolation: Concurrent execution of transactions leads same state as they were executed sequentially.
+ Durability: Once a transaction has been committed, it will remain committed even in the case of a system failure.

Note that Consistency in ACID differs from Consistency in CAP.
Consistency in CAP is that the data in every nodes of a distributed system must be consistent before read, to make sure all reads contain the most recent write.


## BASE

+ Basically Available: Same concept as Availability in CAP. Every request from client receives a non-error response.
+ Soft state: Due to the lack of immediate consistency, data values may change over time, even without receiving requests.
+ Eventually consistency: Consistency here is same as in CAP. Components in distributed systems may not have the latest data due to connection failure. But after some period of time, all nodes will eventually updated to most recent write. This compromise has some advantage on Availability.

## Conclusion

No distributed system is safe from network failures, thus network partitioning generally has to be tolerated. In the presence of a partition, one is then left with two options: consistency or availability.
1. Choose availability over consistency: Data replica in every component may not contain latest change. Is this acceptable? How much can users tolerate?
2. Choose consistency over availability: Service will be suspended if any component has network issues. Will it impact users? How long is acceptable for users?

We can see that CAP Theorem is more about balance. Choose a sweet point that fits user requirements the most.

# Reference
> https://www.zhihu.com/tardis/zm/art/607913356?source_id=1003
> https://ithelp.ithome.com.tw/articles/10216500
> https://rickhw.github.io/2020/05/16/DistributedSystems/Distributed-Transactions/