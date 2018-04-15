---
layout: post
title:  "Comparing the Performance of Web Server Architectures: Review"
date:   2018-01-29 08:00:00
author: Souptik Sen
---

## Summary
<p>
Threads vs process is an ongoing debate in designing computer systems. Depending upon the workload, and the nature of the application, it might be better to design it in a multi-process way vs a multithreaded way or vice versa. The paper presents a thorough performance-oriented evaluation of web-server architectures comparing event-driven, thread-per-connection, and hybrid pipelined server architectures. They use the fastest available server for each architecture, apply some modifications (like using zero copy sendfile) and demonstrate the importance of properly tuning each server appropriately. They show how they modified Knot, enabling it to use sendfile system call, both in blocking and non-blocking mode. Also they modified u-server to act as a SYMPED (symmetric multiple process event-driven) server, which yields much lower CPU utilization. The tuning part is very important, because the performance of each server is affected by the number of concurrent connections and kernel threads. The authors put a lot of emphasis in making the different systems comparable by using the same programming language, and having common components for caching, hashing etc. After thoroughly testing and benchmarking, they conclude that the u-server and Watpipe have a 18% higher throughput than knot (multithreaded) server.
</p>


## What I liked about this paper
<p>
a.  The authors spent very great effort to get the three different architectures to a comparable level. They changed the knot server to use the sendfile system call and implemented their own pipelined server (WatPipe) in C++. <br>
b.  The authors demonstrated the importance of properly tuning each server to get the best results. They provide elaborate testing schemes and compare server throughput and response times for each.<br>
c.  The authors show exact representation of results in graphs. One thing we can see is that the graphs start at X axis =0, which is different from the Flash paper where they put X=200 as the starting point, thus being able to embellish their results slightly.
</p>

## Critical comments
<p>
a.  It would be great to see how these results might differ in a multiprocessor environment. The authors mention in the paper about this – “It will be interesting to see if the current efficiencies in Capriccio can be maintained in an environment that supports multiprocessors or if such support necessarily introduces new inefficiencies.”, but don’t go into detail in explaining the results/consequences.<br>
b.  Web server performance tests are very dependent on how often you hit the disk. But we see no discussions on this (like measuring seek rate, cache hit rate, how worn out are the disks after millions of ops).<br>
Some Systems concepts could be explained better so that the paper is better understandable for someone who is not into OS research (e.g., how do poll and epoll work, etc.)
</p>

## Questions
<p>
a.  How will the results differ if we take multiprocessor systems into account? <br>
b.  We can see that the optimal performance of the Webservers has been achieved by carefully hand-tuning the systems manually. Can this process be automated? 
</p>
