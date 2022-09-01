---
title: RESTful API Brief Introduction
tags:
---

Representational State Transfer (REST) architectural style has been first presented in 2000 in dissertation *Architectural Styles and the Design of Network-based Software Architectures* by Roy Fielding.\
Which introduced and elaborated the REST architectural style for distributed hypermedia systems.
He is also one of the principal authors of HTTP/1.1 specification.

{% asset_img Roy-Fielding.jpg Roy Fielding %}

<!-- more -->

## REST Guiding Principles

**REST principles indicate how to use HTTP properly.**

If an application **completely** compliant with REST principles, can be called
+ RESTful Web Service
+ RESTful Web API

There are 5+1 REST Constraints:
+ Client-Server
+ Stateless
+ Cacheable
+ Uniform Interface
+ Layered System
+ Code on Demand (Optional)

### Client-Server
Decouple client and server using uniform interface between them.

Separation of concerns is the principle behind the client-server constraints:

API Provider (data storage concerns)
+ Cache
+ Performance
+ Scaling
+ Data Security
+ Authentication
+ Authorization

API Consumer (user interface concerns)
+ User Experience
+ User Interface
+ Multi Platform Support

### Stateless
Each request from the client to the server must contain all of the information necessary to understand and complete the request.\
The server does not store any previous context or state information.\
The client must keep the session state.

Advantages:
+ Visibility (a monitoring system does not have to look at requests before)
+ Reliability (easier to recover from partial failures)
+ Scalibility (server does not have to store state between requests)

Trade-offs:
+ Over-communicate
+ Decrease performance (increasing repetitive data)

### Cache
Response should implicitly or explicitly label itself as cacheable or non-cacheable.\
If the response is cacheable, the client application gets the right to reuse the response data later for equivalent requests and a specified period.\
Cache have the potential to partially or completely eliminate some interactions. And can be implemented in any layer of Layered System

Advantages:
+ Efficiency
+ Scalibility

Trade-offs:
+ Decrease reliability (if stale data within the cache differs)

### Uniform Interface
There are 5 key points for understanding Uniform Interface.

#### Resource
The key **abstraction of information** in REST is a resource.\
Any information that we can name can be a resource.\
Server is treated as many discrete resources.

A resource can be identified by one or multiple URIs (Uniform Resource Identifier).\
URI is the name of the resource, also an address on Web.

#### Representation
Representation of resource describes the **state of resource at a specific time**.\
Which can be in multiple formats (HTML, XML, JSON, text, picture, video, audio...)

#### State Transfer
Transfer representation of resource between client and server.\
Control resource inderectly by transfering and operating representation of resource.

#### Self-descriptive Messages
Each resource representation should carry enough information to describe how to process the message.\
It should also provide information of the additional actions that the client can perform on the resource.

#### Hypermedia as the engine of application state (HATEOAS)
The client should have only the initial URI of the application.\
The client is able to reach the next resources and interactions with the use of hyperlinks.


### Layered System
Client-Server Architecture is already a layered system.\
Layer can be created, deleted, and modified based on requirements.

Each Layer is independent to each other (Decoupling).\
Each component cannot see beyond the immediate layer they are interacting with (Law of Demeter a.k.a. Principle of Least Knowledge).

### Code on Demand (Optional)
Client functionality can be extended by downloading and executing code in the form of applets or scripts.\
Which simplifies clients by reducing the number of features required to be pre-implemented.

In current Web design is JavaScript, others like JAVA, Flash, ActiveX...

## Richardson Maturity Model
RMM from Martin Fowler helps checking how RESTful the system is.

{% asset_img REST-Richardson-Maturity-Model.png REST Richardson Maturity Model %}

+ Level 0 stands for HTTP
+ Level 1 breaking a large service endpoint down into multiple resources.
+ Level 2 introduces a standard set of verbs, removing unnecessary variation.
+ Level 3 introduces discoverability, providing a way of making a protocol more self-documenting.

## Epilogue

REST is an architectural style for distributed hypermedia systems.\
But the actual situation may be more complicated than in theory.

REST is just like a screwdriver in your toolbox. It works most of the time but not all the time.
There are multiple ways to fulfill requirements, sometimes even an anti-pattern way.
Requirements are always at first priority, not architecture nor design pattern.

# References

> Roy Fielding, 2000, *Architectural Styles and the Design of Network-based Software Architectures*
> https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm
> RFC2616, RFCs7230-7237
> https://restfulapi.net/
> https://skilltree.my/Events/2022/8/13/Web-API-elementary-net6
> https://martinfowler.com/articles/richardsonMaturityModel.html
