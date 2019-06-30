---
layout: post
title:  "An Updated Performance Comparison of Virtual Machines and Linux Containers : Review"
date:   2018-03-05 05:00:00
author: Souptik Sen
---

## Summary
<p>
Both VMs and containers are mature technology that have benefited from a decade of incremental hardware and software optimizations. Cloud computing makes extensive use of virtual machines (VMs) because they permit workloads to be isolated from one another and for the resource usage to be somewhat controlled. However, the extra levels of abstraction involved in virtualization reduce workload performance, which is passed on to customers as worse price/performance. Newer advances in container-based virtualization simplifies the deployment of applications while continuing to permit control of the resources allocated to different applications.
</p>
<p>
In this paper, the authors take us through the performance of traditional virtual machine deployments, and contrast them with the use of Linux containers. They use a suite of workloads that stress CPU, memory, storage, and networking resources, using KVM as a representative hypervisor and Docker as a container manager. The results show that containers result in equal or better performance than VMs in almost all cases, although both VMs and containers require tuning to support I/O-intensive applications. For I/O intensive workloads, both forms of virtualization should be used carefully. The authors find that KVM performance has improved considerably since its creation. Workloads that used to be considered very challenging, like line-rate 10 Gbps networking, are now possible using only a single core using 2013-era hardware and software. Even using the fastest available forms of paravirtualization, KVM still adds some overhead to every I/O operation; this overhead ranges from significant when performing small I/Os to negligible when it is amortized over large I/Os. Thus, KVM is less suitable for workloads that are latency-sensitive or have high I/O rates. These overheads significantly impact the server applications we tested. Although containers themselves have almost no overhead, Docker is not without performance gotchas. Docker volumes have noticeably better performance than files stored in AUFS. Docker’s NAT also introduces overhead for workloads with high packet rates. These features represent a tradeoff between ease of management and performance and should be considered on a case-by-case basis. In some sense the comparison can only get worse for containers because they started with near-zero overhead and VMs have gotten faster over time. If containers are to be widely adopted they must provide advantages other than steady-state performance. Finally, the authors also discuss the implications of performance results for future cloud architectures.

</p>


## What I liked about this paper
<p>
a.  The authors give a good idea about virtualization and containers, clearly explaining the difference between the 2 technologies.<br>
b.  The experimentation used for comparison of VM vs container performance is extensive and well thought about.<br>
c.  The authors give some great insider insight into when both VMs and containers might not perform well- for example both VMs and containers require tuning to support I/O-intensive applications.
</p>

## Critical comments
<p>
a.  Both VMs and containers require tuning to support I/O-intensive applications.<br>
b.  KVM needs extensive tuning for CPU pages to get a good performance. <br>
c.  The paper doesn’t talk about security evaluation in VMs vs containers.
</p>


## Questions
<p>
a.  How do VMs and containers compare in terms of security?<br>
b.  What are some good tuning practices to extract maximum I/O performance from KVMs?<br>
c.  Discuss the role of containerization in machine learning workloads.
</p>
