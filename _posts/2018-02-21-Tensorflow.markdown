---
layout: post
title:  "TensorFlow: A system for large-scale machine learning: Review"
date:   2018-02-21 05:00:00
author: Souptik Sen
---

## Summary
<p>
The paper introduces TensorFlow which is an open source software library for numerical computation using data flow graphs. The graph nodes represent mathematical operations, while the graph edges represent the multidimensional data arrays (tensors) that flow between them. This flexible architecture lets us deploy computation to one or more CPUs or GPUs in a desktop, server, or mobile device without rewriting code. While in previous “parameter server” designs the management of shared state is built into the system, TensorFlow enables developers to experiment with novel optimizations and training algorithms. TensorFlow supports a variety of applications, with a focus on training and inference on deep neural networks. This paper provides an in-depth description of the dataflow model as well as performance metrics on key large scale machine learning problems from the domain of language modelling and image classification. It also talks about fault tolerance and the approach to mitigate stragglers.
</p>


## What I liked about this paper
<p>
a.  The principal limitation of batch dataflow systems is that they require the input data to be immutable and computations to be deterministic. However even though TensorFlow is based on the dataflow architecture, it exploits mutable state to perform the functionality of a parameter server, and provide additional flexibility.<br>
b.  The paper gives some thoughtful real world examples to demonstrate the working of TensorFlow along with performance characteristics. These examples, taken from a wide variety of network architectures from language models to image classification nets, give a fairly good idea of the dataflow paradigm used in TensorFlow.<br>
Good collection of real world examples to explain the use case of Dataflow model (micro-batch, batch and streaming cases like billing, statistics calculations and anomaly detection).
</p>

## Critical comments
<p>
a.  The paper doesn’t talk about accuracy of the models and how it changes with respect to increasing the number of workers or parameter servers.<br>
b.  The paper cites Google’s predecessor to TensorFlow- the DistBelief system very often but doesn’t give a comprehensive description of the system to the reader.<br>
c.  The paper doesn’t compare the performance (number of iterations for convergence, convergence time, final convergence accuracy) with respect to immutable dataflow based systems like Spark (SparkNet). Since Spark does a better job of dealing with stragglers and tolerating failures, we need to take a look at how these factors affect the performance of TensorFlow systems.
</p>


## Questions
<p>
a.  Spark does a great job of dealing with stragglers and tolerating failures. In a cluster where stragglers and node failures are very common, how will the performance of a TensorFlow based network be with respect to something like SparkNet? Will adding backup tasks outperform the advanced straggler mitigation techniques employed by Hadoop.<br>
b.  What is the “sampled softmax” algorithm cited in 6.4? <br>
c.  How does the model converge in presence of asynchronous gradient updates by the workers to the Master?
</p>
