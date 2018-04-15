---
layout: post
title:  "The Google File System: Review"
date:   2018-02-11 05:00:00
author: Souptik Sen
---

## Summary
<p>
The paper describes the Google File System for supporting large-scale data processing workloads on commodity hardware. The data processing needs of Google required a file system addressing all the usual goals such as performance, scalability, reliability and availability, but with different design philosophies. During the development of GFS there are some key observations that make the design different from previous file system design assumption. First the failure of component is normal not exception, since the commodity hardware is inexpensive and as the scale of the system is large. That virtually guarantee failures in either software hardware or operation. Therefore, constant monitoring, error detection and automatic recovery must be considered.
</p>

## What I liked about this paper
<p>
a.  This was probably the first example of a large scale file system that is built on cheap commodity hardware, yet it is resilient to failures and optimized for large files. <br>
b.  A new and innovative concept is the usage of lease given to a primary chunkserver, and the expiration term that comes handy in case of chunkserver failure. <br>
c. Previously all file systems stored files within a Directory structure. In GFS, such a Directory structure doesn't exist. The master maps pathnames to chunks through an in-memory compressed lookup table. <br>
</p>

## Critical comments
<p>
a.  All metadata is stored in Master, won't this be a Single point of failure if the Master dies? Since only the master knows all the metadata maps, any downtime of the master leads to downtime of the whole cluster.<br>
b.  GFS is highly optimized for Google's data access patterns. It would have been better if they could make this generic for general purpose file systems.<br>
c.  Having metadata in master's main memory, all lookup operations are fast. But could this limit the size of the whole cluster because there is a limit to the master's main memory?
</p>

## Questions
<p>
a.  High Availability mode for Master: Can we extend the File system design to have multiple Masters? So that the hole cluster doesn't have to endure downtime because of master failure. Kind of like having a backup Master. <br>
b.  In case of HA mode for Master, the backup Master will have to consistently update its own metadata with the original Master. What would be a good replication strategy for this?<br>
c.  Active-active Masters: As I mentioned there is a limit the size of the whole cluster because there is a limit to the master's main memory. Backup master doesn't solve the problem, because it is an exact replica to the Master. Can we use an Active-active mechanism instead having 2 (or multiple) Masters balancing load amongst each other? What could be some of the potential designs for this?
</p>