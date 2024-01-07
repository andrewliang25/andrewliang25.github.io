---
title: Fundamentals of Garbage Collection in .NET
tags:
---

The common language runtime (CLR) provides an automatic memory manager, which is the garbage collector (GC).
Unlike languages like C and C++, developers need to manually handle memory allocation, the GC manages the allocation and deallocation of memory for objects in a .NET application to simplify development, reduce memory leaks, and improve overall code safety.

{% asset_img dotnet_logo.png .NET logo %}


<!-- more -->


## Benefits

The garbage collector provides the following benefits:

+ Frees developers from having to manually release memory.

+ Allocates objects on the managed heap efficiently.

+ Reclaims objects that are no longer being used, clears their memory, and keeps the memory available for future allocations. Managed objects automatically get clean content to start with, so their constructors don't have to initialize every data field.

+ Provides memory safety by making sure that an object can't use for itself the memory allocated for another object.


## When does Garbage Collection occur?

Garbage collection occurs when one of the following conditions is true:

+ The system has low physical memory. The memory size is detected by either the low memory notification from the operating system or low memory as indicated by the host.

+ The memory that's used by allocated objects on the managed heap surpasses an acceptable threshold. This threshold is continuously adjusted as the process runs.

+ The `GC.Collect()` method is called. In almost all cases, you don't have to call this method because the garbage collector runs continuously. This method is primarily used for unique situations and testing.


# Reference
> https://learn.microsoft.com/en-us/dotnet/standard/garbage-collection/fundamentals
> https://www.site24x7.com/learn/garbage-collection-in-net-framework.html