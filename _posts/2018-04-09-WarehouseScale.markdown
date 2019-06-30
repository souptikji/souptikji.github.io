---
layout: post
title:  "The Datacenter as a Computer- An Introduction to the Design of Warehouse-Scale Machines: Review"
date:   2018-04-09 11:00:00
author: Souptik Sen
---

## Summary
<p>
Today, computing and storage are moving from PC-like clients to smaller, often mobile devices, combined with large Internet services. The move is slowly shifting towards Software as a service, rather than just static webpages. In this scenario, the application software that run on warehouse-scale computers (WSCs) dictate the system design decisions.
</p>
<p>
There are 3 different software layers in a typical WSC deployment- Platform-level software, Cluster-level infrastructure, Application-level software. Platform-level software refers to the common firmware, kernel, operating system which power these large scale services (eg. GFS). Cluster-level infrastructure is the collection of distributed systems software that manages resources and provides services at the cluster level eg. YARN, Borg. Application-level software refers to the software that implements a specific service, like Google search, Gmail, and Google Maps.  This increase in the breadth of services offered has resulted in a much larger diversity of application-level requirements. A search workload may not require an infrastructure capable of high-performance atomic updates and is inherently forgiving of hardware failures (because absolute precision every time is less critical in Web search).  This is not true for an application that tracks user clicks on sponsored links (ads). Thus the datacenter must be a general-purpose computing system. Although specialized hardware solutions might be a good fit for individual parts of services, the breadth of requirements makes it less likely that specialized hardware can make a large overall impact in the operation. 
</p>
<p>
In this chapter the authors also discuss at a high level two workloads that exemplify two broad classes of applications: online services and batch (offline) processing systems. Here we outline the basic architecture of a Web-search application as an example of an online system and a citation-based similarity computation that uses MapReduce as an example of a batch workload.
</p>


## What I liked about this paper
<p>
a.  The authors give a good insight and intuition into how internet services scale programming differs from desktop/server models by talking about parallelism, workload churn, platform homogeneity and fault free operation.<br>
b.  The table on performance and availability toolbox is really intuitive on how different techniques provide value in large scale internet services. I liked the description of canaries- have always found it confusing but the authors have explained it clearly here.<br>
c.  The authors also give a detailed analysis about the workloads of 2 real-life applications at Google (search and citation summary) and how it is used to make design tradeoffs.
</p>

## Critical comments
<p>
a.  Thread level parallelism is not leveraged in internet services.<br>
b.  The paper talks about Reed-Solomon codes being used to allow recovery form data losses with less space overhead than straight replication. But in datacenters there is a requirement of both throughput as well as fast availability.<br>
c.  The chapter doesn’t talk about Machine learning workloads.
</p>


## Questions
<p>
a.  In large scale ML jobs, if a particular task fails (or straggles) then there is usually no need to re-execute (different from data related jobs) and it can usually tolerate the staleness. How does this workload affect the system design tradeoffs?<br>
b.  How to provide high availability as well as throughput in datacenters?<br>
c.  How does the workload of OLAP jobs influence the system design?
</p>
