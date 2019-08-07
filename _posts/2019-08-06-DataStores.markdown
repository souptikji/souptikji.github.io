---
layout: post
title:  "MTV CS Reading Group: Data structures that power your database"
date:   2019-08-06 05:00:00
author: Souptik Sen
---

# Core topic of discussion

 Today we discussed Chapter 3 from Martin Kleppman's book *"Designing Data Intensive Applications"* . Fundamentally a data store needs to do two things: when you give it some data, it should store the data, and when you ask it again later, it should give the data back to you. This was the focus of our discussion- the various data structures that speed up writing to and querying from a database. We learnt about 2 families of datastructures used for indexing - Log based and page based 


# Log based indexing

We read about Hash index and SStable based indexing (LSM trees). Main point - useful for write heavy applications, but reads might be slower. The idea behind Hash index is to store a mapping of keyset in memory pointing to the value reference (which might be a row or a json file whatever). The idea behind SSTables is usage of sparse indices thanks to sorting the key set, also good for lookups.

# Page based indexing

We read about BTrees. Like SSTables, B-trees keep key-value pairs sorted by key, which allows efficient key- value lookups and range queries. While LSM-trees are typically faster for writes, whereas B-trees are thought to be faster for reads.

# BTrees vs LSM trees comparison

Please refer to the below diagram for our comparison points between LSM trees and B Trees-
![](btreevslsm.jpeg)

