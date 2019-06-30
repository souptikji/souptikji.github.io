---
layout: post
title:  "kqueue versus epoll: A Performance Comparison: Review"
date:   2018-01-30 11:00:00
author: Souptik Sen
---

## Summary
<p>
Modern high-performance webserver architectures often use an event driven concurrency model. Their scalability and performance depends a lot on efficiency of event notification and delivery. In this paper the authors experimentally evaluated two popular, scalable I/O notification primitives present in Unix-based server operating systems. They find the claims of performance improvement over traditional primitives to hold true for a wide range of benchmarks. At the same time, applications using the Linux notification API may suffer excessive system calls for specific inter-arrival patterns - a deficiency the BSD API does not seem to exhibit. However, kqueue’s relatively more complex API may be harder to program with and lead to subtle correctness issues if used without caution.</p>


## What I liked about this paper
<p>
a. The authors document the challenges they faced while doing the benchmark which is interesting to read.<br>
b. The experimental testbed and results have been properly explained. I really liked the Kernel distribution of CPU time spent per system call analysis.<br>
c. System call scalability analysis is also very interesting.
</p>

## Critical comments
<p>
a. Although the experimentation is exhaustive, I saw that a lot of benchmarks already been done in this area in many academic papers and tech blogs.<br>
b. It would have been great to see benchmarking results for different platforms.<br>
The background on epoll and kqueue system calls might not be accessible to someone with elementary OS/systems knowledge.
</p>


