---
title: "Understanding Android Memory Management: A Comprehensive Guide"
seoTitle: "Android Memory Management: Comprehensive Guide"
seoDescription: "Guide to Android memory management: Optimize resources, improve performance, and enhance user experience"
datePublished: Fri May 05 2023 08:26:08 GMT+0000 (Coordinated Universal Time)
cuid: clhaakokt000409lc5kzm6t7t
slug: understanding-android-memory-management-a-comprehensive-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1682195852536/f37f70a3-7544-45f9-8321-77e4fe432d54.png
tags: android, memory-management, garbagecollection, operatingsystems, memorymanagement

---

## I. Introduction

Memory management in operating systems is the process of managing the RAM (Random Access Memory) and ensuring that each process and application has access to the required amount of memory.

It involves allocating memory when a process or application needs it, freeing up memory when it is no longer required, and preventing memory leaks and other issues that can arise from inefficient memory usage.

Every Operating system has its own way of managing memory so does Android. The foundation of the Android platform is the Linux kernel. the Android Runtime (ART) relies on the Linux kernel for underlying functionalities such as threading and low-level memory management.

![](https://developer.android.com/static/guide/platform/images/android-stack_2x.png align="center")

Efficient memory management helps to ensure that each process and application has access to the required amount of memory, preventing memory leaks and other issues that can arise from inefficient memory usage.

It also helps to conserve battery life by reducing unnecessary memory usage. Overall, proper memory management is essential for a smooth and efficient user experience on Android devices.

In this blog, we will cover how the system manages memory internally.

## II. Types Of Memory

Android has 3 Types of Memory. Ram, zRam & Storage

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683316868875/4ab9b5a3-ce02-43f5-8b98-b6bbd6e7c607.png align="center")

* **RAM:** it's the fastest type of memory, but is usually limited in size. High-end devices typically have the largest amounts of RAM. This is the prime memory that handles all ongoing operations.
    
* **zRAM:** It's a partition of RAM used for swap space. Everything is compressed when placed into zRAM, and then decompressed when copied out of zRAM. This portion of RAM grows or shrinks in size as pages are moved into or taken out of zRAM. Device manufacturers can set the maximum size.
    
* **Storage**: It contains all of the persistent data such as the file system and the included object code for all apps, libraries, and the platform. Storage has much more capacity than the other two types of memory. On Android, storage isn’t used for swap space like it is on other Linux implementations since frequent writing can cause wear on this memory, and shorten the life of the storage medium.
    

## III. Memory Pages

RAM is broken up into *pages*. Typically each page is 4KB of memory.

Pages are considered either ***free*** or ***used***. Free pages are unused RAM. Used pages are RAM that the system is actively using, and are grouped into the following categories:

1. **Cached**: Memory backed by a file on storage (for example, code or memory-mapped files). There are two types of cached memory:/
    
    * **Private: Owned by one process and not shared**
        
        * *Clean: Unmodified copy of a file on storage, can be deleted by* `kswapd` *to increase free memory*
            
        * *Dirty: Modified copy of the file on storage; can be moved to, or compressed in, zRAM by* `kswapd` *to increase free memory*
            
    * **Shared: Used by multiple processes**
        
        * Clean: Unmodified copy of the file on storage, which can be deleted by `kswapd` to increase free memory
            
        * Dirty: Modified copy of the file on storage; allows changes to be written back to the file in storage to increase free memory by `kswapd`, or explicitly using [`msync()`](https://developer.android.com/reference/android/system/Os#msync(long,%2520long,%2520int)) or [`munmap`](https://developer.android.com/reference/android/system/Os#munmap(long,%2520long))
            

---

1. **Anonymous**: Memory **not** backed by a file on storage (for example, allocated by [`mmap()`](https://developer.android.com/reference/android/system/Os#mmap(long,%2520long,%2520int,%2520int,%2520java.io.FileDescriptor,%2520long)) with the `MAP_ANONYMOUS` flag set)
    
    it is a Dirty page that can be moved/compressed in zRAM by `kswapd` to increase free memory
    

## IV. Low Memory Killer

When free memory falls below the low threshold, `kswapd` starts to reclaim memory. Once the free memory reaches the high threshold, `kswapd` stops reclaiming memory.

**Clean Page :** `kswapd` can reclaim clean pages by deleting them because they're backed by storage and have not been modified.

If a process tries to address a `clean` page that has been deleted, the system copies the page from storage to **RAM**. This operation is known as [`demand paging`](https://www.javatpoint.com/os-demand-paging).

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683316887713/bf7b726f-e5f5-4e71-be4b-8cca88b19a8e.png align="center")

---

**Dirty Pages:** `kswapd` can move cached private **dirty** pages and anonymous dirty pages to zRAM, where they are compressed. Doing so frees up available memory in RAM (free pages).

If a process tries to touch a dirty page in zRAM, the page is uncompressed and moved back into RAM. If the process associated with a compressed page is killed, then the page is deleted from zRAM.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683316899299/9cf4e70b-400e-478d-895b-1722e19662e3.png align="center")

---

If the amount of free memory falls below a certain threshold, the system starts killing processes. To decide which process to kill, LMK uses an "out of memory" score called [`oom_adj_score`](https://android.googlesource.com/platform/system/memory/lmkd/+/master/README.md) to prioritize the running processes.

Processes with a high score are killed first. Background apps are first to be killed, and system processes are last to be killed. The following table lists the LMK scoring categories from high-to-low. Items in the highest-scoring category, in row one, will be killed first:

### V. Garbage Collection

Garbage collection in Android identifies and releases memory that is no longer being used by the app, helping to prevent memory leaks and ensure efficient memory usage.

It involves marking live objects in the heap, traversing the object graph to mark all reachable objects, sweeping away unreachable objects to free up memory, and compacting remaining live objects to reduce memory fragmentation.

In Android Garbage collection runs when System want to release the app completely from the heap or while the user using the app if any object reference is not required any more.

## VI. Switch Apps

When users switch between apps, Android keeps apps that are not foreground—that is, not visible to the user or running a foreground service like music playback— in a cache.

For example, when a user first launches an app, a process is created for it; but when the user leaves the app, that process does *not* quit. The system keeps the process cached. If the user later returns to the app, the system reuses the process, thereby making the app switching faster.

If your app has a cached process and it retains resources that it currently does not need, then your app—even while the user is not using it— affects the system's overall performance.

As the system runs low on resources like memory, it kills processes in the cache. The system also accounts for processes that hold onto the most memory and can terminate them to free up RAM.

**Note:** The less memory your app consumes while in the cache, the better its chances are not to be killed and to be able to quickly resume. However, depending on instantaneous system requirements, it's possible for cached processes to be terminated at any time no matter their resource utilization.

---

In conclusion, understanding Android memory management is crucial for optimizing app performance and ensuring a smooth user experience.

By learning about the types of memory, memory pages, low memory killer, garbage collection, and app switching, developers can create efficient apps that make the best use of available resources.

Proper memory management helps conserve battery life and reduces the likelihood of app termination due to low memory conditions.

---

That's all for now. If you enjoyed the article, please give it a thumbs up. Thank you for reading! :)