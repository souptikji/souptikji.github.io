---
layout: post
title:  "MapReduce: Simplified Data Processing on Large Clusters: Review"
date:   2018-02-15 05:00:00
author: Souptik Sen
---

## Summary
<p>
The MapReduce paper is one of the pioneers in the field of large scale data processing. The paper describes a new programming model based on functional programming's map and reduce primitives for processing large data set, thereby providing an abstraction that hides many system-level details from the programmer. This paper describes the various error scenarios that happen in a large cluster of commodity hardware machines as well as various performance improvements that are added to the framework.
</p>


## What I liked about this paper
<p>
a.  The innovate concept of using pure functions (functions without any side-effects) from the functional programming world for fault tolerance (running mappers, reducers multiple times on the same data).<br>
b.  Instead on moving data from multiple machine to be processed by a function, the application master moves the mapper functions to the data nodes. This is a vibrant example of “moving code to data” and shows the tremendous performance benefits.<br>
c.  The biggest contribution of the paper is that it provides an abstraction that hides many system-level details from the programmer/data scientist. So a ML practitioner with limited knowledge of parallel programming, doesn’t have to learn the internals to implement his/her solution.

</p>

## Critical comments
<p>
a.  Application master is still the single point of failure. <br>
b.  Each stage spits data into GFS and reads from GFS, thereby imposing a tremendous disk/network bottleneck. <br>
c.  MapReduce API although succinct, is very limited in power. Functional programming primitives like flatMap, groupByKey, reduceByKey, etc. have to be written by the programmer from scratch. <br>
d.  Mapreduce doesn’t talk about how it can handle security- that is, work on a cluster of untrusted or possibly malicious computer systems.

</p>

## Questions
<p>
a.  How can we run Map reduce in a cluster on untrusted/ unreliable computers? It would be great if we come up with a service that takes some computational power/ space in user’s mobile phones to assign mapper/reducer tasks in them. What can be the challenges in such an approach? <br>
b.  In figure 3c, we see that the input, shuffle and output data rate in MBps drops below zero. How is that possible? <br>
c.  Active-active Masters: As How can we change map-reduce cluster to have multiple masters? Maybe one can be active while the other passively copies state from the main master. Or can we also have an Active-Active master scenario?

</p>
