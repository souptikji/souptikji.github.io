---
layout: post
title:  "The Dataflow Model: A Practical Approach to Balancing Correctness, Latency, and Cost in Massive-Scale, Unbounded, Out-of-Order Data Processing: Review"
date:   2018-02-19 05:00:00
author: Souptik Sen
---

## Summary
<p>
The paper talks about Google Dataflow which is a new programming model that can express streaming, micro-batch, batch and other processing models (along with providing functionality on them like windows and triggers). The challenge with correctness of streaming systems is data coming late or out of order (dues to stragglers, network partitions, etc.). If we care about correctness and are interested in analyzing your data in the context of their event times, we cannot define those temporal boundaries using processing time (i.e., processing time windowing), as most existing systems do; with no consistent correlation between processing time and event time, some of your event time data are going to end up in the wrong processing time windows (due to the inherent lag in distributed systems, the online/offline nature of many types of input sources, etc.), throwing correctness out the window.</p>
<p>
In Dataflow, the developers could specify their processing behavior (streaming, micro-batch, batch, etc.) by tuning the appropriate knobs (completeness vs latency vs cost). With its powerful API, Dataflow provides what MapReduce and other batch systems are missing- low latency as well as an ability to have a continuous data flow. At the same time these knobs are tunable to give us a batch processing pipeline too. It supports the unaligned, event-time-ordered windows modern data consumers require. It provides flexible triggering and integrated accumulation and retraction, refocusing the approach from one of finding completeness in data to one of adapting to the ever present changes manifest in real world datasets.
</p>


## What I liked about this paper
<p>
a.  The authors identify that any batch, micro-batch or streaming approach stems from appropriately tuning 3 tradeoffs- completeness vs latency vs cost. This kind of simplicity gives a solid foundation to the data model.<br>
b.  The API provided by the Dataflow on Triggers and incremental processing is very powerful. Especially the Accumulating & Retracting API which is not covered by many streaming systems like Spark streaming.<br>
Good collection of real world examples to explain the use case of Dataflow model (micro-batch, batch and streaming cases like billing, statistics calculations and anomaly detection).
</p>

## Critical comments
<p>
a.  The paper doesn’t talk about any results of the system or how it compares to other streaming or batch models. No performance evaluation.<br>
b.  The paper is not written very clearly and many terms are confusing.<br>
c.  No discussion of fault tolerance mechanisms in batch or streaming mode.
</p>


## Questions
<p>
a.  How does the performance of Dataflow compare with traditional batch (Hadoop MR/Spark) or streaming (Kafka, Spark Streaming) systems?<br>
b.  How is the heuristic for watermark calculated? <br>
c.  What kind of fault tolerance mechanisms are used in batch or streaming mode?
</p>
