---
title: 'Comparison of Asynchronous Messaging: JMS, AMQP and MQTT'
date: 2024-02-05 16:18:54
tags:
---


Asynchronous messaging is that sender does not expect an immediate response and does not “blocks” waiting for the response. He will carry out his remaining tasks.

This article will introduce common patterns and compare 3 popular technologies for asynchronous messaging.

## Asynchronous messaging patterns

There are two basic patterns in asynchronous messaging (and more variants):

1. Message queue
{% asset_img message-queue-pattern.jpg Message queue %}
Using `queue` as a message broker. One message can only be consume by a consumer. Unconsumed messages will be stored in queue until timeout.

<!-- more -->

2. Publish/subscribe
{% asset_img pub-sub-pattern.png Publish/subscribe %}
When a message is published, it is send to all subscribers who subscribed to the `topic` of the message.


## Java Messaging Service (JMS)

JMS has been one of most successful asynchronous messaging technology available. With the growth of the Java adoption of large enterprise applications, JMS has been the first choice for enterprise systems. It defines the API for building the messaging systems.

+ A standard messaging API for Java platform.
+ Supports two messaging models: `queue` and `topic`.
+ Supports transactions, message format, and long-lived store.
+ Not interoperable with other platforms or languages, and does not define a wire level protocol.


## Advanced Message Queueing Protocol (AMQP)

There was no standard wire level protocol with JMS. And AMQP provided a standard wire level protocol and many other features to support the interoperability and rich messaging needs for the modern applications.

+ A platform-independent wire level messaging protocol.
+ Supports consumer-driven messaging, interoperability, buffer-oriented performance, and distributed transactions.
+ 5 exchange types: `direct`, `fanout`, `topic`, `headers`, and `system`.
+ Complex and not suitable for small devices or low bandwidth networks.


## Message Queueing Telemetry Transport (MQTT)

Devices with less computing power cannot deal with all the complexities of AMQP rather they want a simplified but interoperable way to communicate.
This was the fundamental requirement for MQTT.

+ A stream-oriented, low memory consumption messaging protocol.
+ Supports publish-subscribe for topics, ephemeral messaging, and last value queue.
+ Simple security and global namespace.
+ Not support transactions, long-lived store, fragmented messages, or connection security.


# Reference

> https://javaguide.cn/high-performance/message-queue/message-queue.html#jms-%E5%92%8C-amqp
> https://chanakaudaya.medium.com/comparison-of-asynchronous-messaging-technologies-with-jms-amqp-and-mqtt-4f1bc21c26c5
> https://blogs.mulesoft.com/migration/asynchronous-messaging-patterns
> https://medium.com/@miladev95/message-broker-and-rpc-c0b1906738b1
> https://www.cloudamqp.com/blog/what-is-message-queuing.html
> https://aws.amazon.com/what-is/pub-sub-messaging