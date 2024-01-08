---
title: Fundamentals of Garbage Collection in .NET
date: 2024-01-08 15:01:08
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

+ Reclaims objects not used and clears their memory for future allocation.

+ Provides memory safety.


## Fundamentals of memory

Common language runtime (CLR) memory concepts:

+ Each process has its own, separate virtual address space. All processes on the same computer share the same physical memory and the page file, if there is one.

+ By default, on 32-bit computers, each process has a 2-GB user-mode virtual address space.

+ Application developers work only with virtual address space and never manipulate physical memory directly.The garbage collector allocates and frees virtual memory on the managed heap.

+ Virtual memory can be in three states:

	+ Free: The block of memory has no references to it and is available for allocation.
	+ Reserved: The block of memory is available for use and cannot be used for any other allocation request. However, cannot store data to this memory block until committed.
	+ Committed: The block of memory is assigned to physical storage.


+ Virtual address space can get fragmented.

+ Run out of memory if there is not enough virtual address space to reserve or physical space to commit.


## When does Garbage Collection occur

+ Low physical memory.

+ The memory used surpasses an acceptable threshold.

+ The `GC.Collect()` method is called.


## The managed heap

After the CLR initializes the garbage collector, it allocates a segment of memory to store and manage objects. This memory is called the managed heap.

The fewer objects allocated on the heap, the less work the garbage collector has to do.

When a garbage collection is triggered, the garbage collector reclaims the memory that is occupied by dead objects. The reclaiming process compacts live objects so that they are moved together, and the dead space is removed, thereby making the heap smaller.

The heap can be considered as the accumulation of two heaps:
+ Small object heap
+ Large object heap (LOH): Contains objects that are 85,000 bytes and larger, which are usually arrays. It is rare for an instance object to be extra large.


## Object Generations

The GC algorithm is based on several considerations:
+ Compacting a portion of the managed heap is faster than the entire managed heap.
+ Newer objects have shorter lifetimes, and older objects have longer lifetimes.
+ Newer objects tend to be related to each other and accessed by the application around the same time.

To optimize the performance of the garbage collector, the managed heap is divided into three generations, 0, 1, and 2, so it can handle long-lived and short-lived objects separately.

+ Generation 0: The youngest generation and contains short-lived objects such as temporary variables. Garbage collection occurs most frequently in this generation.
Newly allocated objects form implicitly Generation 0 collections. However, large objects go on the large object heap.

+ Generation 1: This generation contains short-lived objects and serves as a buffer between short-lived objects and long-lived objects. After the garbage collector performs a collection of generation 0, it compacts the memory for the reachable objects and promotes them to Generation 1. Garbage collection in Generation 1 and Generation 2 only occurs if more memory needs be reclaimed after Generation 0 is garbage collected.

+ Generation 2: Contains long-lived objects such as static data. The large object heap, which is sometimes referred to as generation 3, is collected as part of Generation 2.

Objects that are not reclaimed in a garbage collection (a.k.a. survivors) and are promoted to the next Generation.

When the garbage collector detects that the survival rate is high in a generation, it increases the threshold of allocations for that generation. The next collection gets a substantial size of reclaimed memory.

The CLR continually balances two priorities:
1. Not letting a working set get too large by delaying garbage collection.
2. Not letting the garbage collection run too frequently.


## What happens during a garbage collection

1. Marking phase: Finds and creates a list of all live objects.

{% asset_img marking.png Marking %}

2. Relocating phase: Updates the references to the objects that will be compacted.

3. Compacting phase: Reclaims the space occupied by the dead objects and compacts the surviving objects by moving objects towards the older end of the segment.

{% asset_img normal-deletion.png Deletion without compacting %}

{% asset_img deletion-with-compacting.png After compacting %}

The large object heap (LOH) is not compacted because copying large objects imposes a performance penalty. LOH is automatically compacted when a memory limit on a container or other runtime configuration options is reached.

Before a garbage collection starts, all managed threads are suspended except for the thread that triggered the garbage collection.
{% asset_img gc-triggered.png Garbage Collection Triggered %}


## Unmanaged resources

For most of the objects, garbage collection can perform the necessary memory management tasks automatically. However, unmanaged resources require explicit cleanup.
The most common type of unmanaged resource is an object that wraps an operating system resource, such as a file handle, window handle, network connection, or database connection.
Although the garbage collector can track the lifetime of a managed object that encapsulates an unmanaged resource, it does not have specific knowledge about how to clean up the resource and how badly it hurts the performance.

## Conclusion

Although the garbage collector implicitly clean up memory to simplify development, it is still important to learn how it works and what is the boundary of it.
To prevent potential performance issues related to memory management, such as memory overhead, fragmentation, and resource lock.


# Reference
> https://learn.microsoft.com/en-us/dotnet/standard/garbage-collection/fundamentals
> https://www.site24x7.com/learn/garbage-collection-in-net-framework.html
> https://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/index.html
