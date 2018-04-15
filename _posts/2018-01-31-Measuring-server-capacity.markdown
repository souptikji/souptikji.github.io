---
layout: post
title:  "Measuring the capacity of a Web server under realistic loads: Review"
date:   2018-01-31 08:00:00
author: Souptik Sen
---

## Summary
<p>
This paper examines the current techniques for measuring capacity of web server in detail and exposes the limitations for those techniques. To overcome this problem, the authors have proposed a new model for synthetic generation of realistic HTTP client requests and using that model they have measured the performance of Web Servers under realistic web traffic load.  First, the paper mentions drawbacks in the present technique- the testbed used for testing the server is not able to generate an excess load. Further, testbed computers used a fix style for generating requests- the think time is fixed. In reality there are a large number of clients which generate bursty traffic (as their think times depend on a variety of factors and have large mean and variance) and peak request rates which exceed the server's capacity. Thus this simple method used for generating synthetic request is not able to model the bursty traffic pattern. Also, if the number of clients is increased, it leads to a client side bottleneck rather than the expected server side bottleneck. All these issues prove that present web-server performance evaluation techniques are not sufficient and thus there is a scope of improvement.
</p>

<p>
Then paper proposes a new scalable method for generating HTTP requests which can easily generate workload exceeding capacity of server as well as bursty workload. In this method, each client machine runs a number of scalable clients- which consists of two processes - 1) the connection establishment process that handles the HTTP request and 2) the connection handling process that handles the HTTP response. The paper describes how the processes handle the HTTP requests based on elapsed time and number of requests. This structure helps to achieve these two things- 1) shortens the TCP connection establishment time out to allow the generation of request rates beyond the capacity of the server with a reasonable number of client sockets and 2) maintains a constant number of unconnected sockets that are trying to establish new connections to ensure that the generated request rate is independent of the rate at which the server handles requests.
</p>


## What I liked about this paper
<p>
a.  The authors rigorously evaluate current methods of generating HTTP traffic and propose a new method after examining the strengths and weaknesses of other methods. The problems that arise while generating synthetic HTTP traffic have been systematically discussed and critiqued. Also they provide a good overview on the dynamics of a typical HTTP server which helps in getting some background knowledge about the problem.<br>
b.  The idea of scalable client that allows them to generate the requests beyond the capacity of server with reasonable number of client sockets, is pretty novel for that time and unique. Their design exploits the way TCP connections work to simulate multiple number of clients which is a very novel way of looking at this problem. <br>
c.  The evaluation of their system is pretty exhaustive- testing on a variety of machines and workloads. Their experiments are a good example of how a good testing scheme at scale should look like.
</p>

## Critical comments
<p>
a.  The presented method generates HTTP requests with a constant think time distribution to achieve a certain constant request rate. The authors mention that "it is possible to generate more complex request processes by adding appropriate think periods between the point where an S-Client detects a connection was established and when it next attempts to initiate another connection". However, will this truly reflect the bursty randomness of client requests?<br>
b.  The authors’ benchmarks don’t take into account request file types, transfer sizes and locality of reference in URLs requested.
</p>

## Questions
<p>
a.  Does this method truly simulate random bursty client requests? <br>
b.  How can we extend the framework further to simulate cyber attacks on servers? Like Denial-of-service attacks, SYN flooding etc.
</p>
