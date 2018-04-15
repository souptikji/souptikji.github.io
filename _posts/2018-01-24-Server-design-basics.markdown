---
layout: post
title:  "Flash: An efficient and portable Web server: Review"
date:   2018-01-24 08:00:00
author: Souptik Sen
---

## Summary
<p>
Threads vs process is an ongoing debate in designing computer systems. Depending upon the workload, and the nature of the application, it might be better to design it in a multiprocess way vs a multithreaded way or vice versa. This paper presents the design of a new Web server architecture called the asymmetric multi-process event-driven (AMPED) architecture, and evaluates the performance of an implementation of this architecture, the Flash Web server. 
</p>

<p>
What are the steps involved in the operation of a simple web server- first, the client or the browser needs to send a request that the web server will accept. After the request is accepted, there are a number of processing steps that the web server needs to perform (reading/parsing the request, finding the file, computing the sending message header, sending the header) before finally responding with the file. Find file and read file events are disk blocking whereas accept connection, read request, send header, send data events are network blocking. Thus a single threaded process for web server spends a lot of time blocked, and is embarrassingly parallel. 
</p>

<p>
One easy way to achieve concurrency is to have multiple instances of the same process. And that way we have a multi-process implementation. Once we have correctly developed the sequence of steps for one process, we just spawn multiple processes. The main downside is memory consumption - processes are heavier than threads and we'll have to allocate memory for every one of them. Other downsides are the context switch time is more expensive for processes and also it can be rather expensive to maintain shared state across processes.
</p>

<p>
An alternative to the multi-process model is to develop the web server as a multi-threaded application. We have multiple execution contexts, multiple threads within the same address space and every single one of them is processing a request. It can also be implemented in a master-slave manner where a single master thread performs the accept connection operation and every single one of the workers performs the remaining operations from the reading of the HTTP request until actually sending the file. The benefits of this approach is that the threads share the address space, so they will share everything that's within it. Also context switching between these threads is cheap and its not memory intensive. The downside of the approach is that it is not simple and straightforward to implement the multi-threaded program. We have to explicitly deal with synchronization when threads are accessing and updating the shared state.
</p>

<p>
The paper then takes us through the event driven model for web server. The application is implemented in a single address space, there is basically only a single process and a single thread of control. The main part of the process is the event dispatcher that continuously in a loop looks for incoming events and then based on those events invokes one or more of the registered handlers. Invoking a handler simply means that we will jump to the appropriate location in the processes address space where the handler is implemented. At that point the handler execution can start. If a handler needs to perform a blocking operation, it will initiate the blocking operation and then it will immediately pass control back to the event dispatcher, so it will no longer be in the handler. At that point, the dispatcher is free to service other events or call other handlers. The way the event-driven model achieves concurrency is by interleaving the processing of multiple requests, within a same execution context. Here in the event-driven model, we have a single thread, and the single thread switches its execution among the processing that's required for different requests. We can see that in the event driven model, a request will be processed in the context of a single thread, as long as it doesn't have to wait. Whenever a wait needs to happen, then the execution thread will switch to servicing another request. However, this is the SPED model (single process event driven), and the disadvantage is that it is blocked on disk reads.
</p>

<p>
Flash is an event-driven webserver that follows the AMPED model- it has asymmetric helper processes to deal with the blocking I/O operations. And then everything else is implemented as an event dispatcher with handlers performing different portions of the web servicing tasks. The communication from the helpers to the event dispatcher is performed via pipes. The helper reads the file in memory via the mmap call, and then the dispatcher checks if the pages of the file are in memory. And it then uses this information to decide if it should just call one of the local handlers, or if it should pass the request to the helper. As long as the file is in memory, reading it won't result in a blocking I/O operation, and so passing it to the local handlers is perfectly okay.
</p>

<p>
There are some other optimizations too that Flash performs. Flash performs application-level caching at multiple levels on both data and computation. Also Flash does some optimizations that take advantage of the networking hardware and the network interface card. For instance, all of the data structures are aligned so that it's easy to perform DMA operations without copying data. Similarly, they use DMA operations that have scatter-gather support, and that really means that the header and the actual data don't have to be aligned one next to another in memory.
</p>


## What I liked about this paper
<p>
1. The paper gives a great insight into the design of high performance web servers (Flash, mu, knot, TUX), giving the positive and negative points of various web server architectures. <br>
2. The paper shows some of the novel performance optimizations (eg. DMA operations that have scatter-gather support in Flash). These ideas might be dated now, but at the time the paper was written they were pretty novel.<br>
3. The authors go into excruciating details of the workloads used for performance testing. This sets a very good example for how testing at scale should be done.
</p>

## Critical comments
<p>
1. The Flash paper is a bit dated and discusses about a static web server where basically the web server just returns static files. The blocking I/O operations that are happening at the system are really just disk reads, but how will this change in today's world, where the content is increasingly dynamic? <br>
2. The paper doesn't mention sendfile(), which has the added performance advantage that the file contents don't even have to be copied into the web server's process memory. 
</p>

## Questions
<p>
a.  How will the flash paper fare in today's world, where the content is increasingly dynamic?
</p>
