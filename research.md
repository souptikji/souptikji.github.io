---
layout: page
title: Research 
permalink: /research/
---

## Areas of Interest
<hr width="850px">
<hr style="height:10pt; visibility:hidden;" />

<p align="justify">
Broadly, my interests lie in the realm of Data Infrastructure, Large scale Machine Learning and Distributed Systems. My current work at LinkedIn involves solving numerous distributed computing challenges using Spark and MapReduce. I am working on optimizing a library (originally written in Java MapReduce, we are rewriting this in Spark) which does massive offline aggregate collection and statistics on Petabytes of LinkedIn data. This aggregated data is then either pushed to visualization tools for Data scientists to slice and dice across dimensions, or used for Machine learning based modeling for recommender systems at LinkedIn. This project is giving me a hands-on experience in writing scalable and efficient Spark and MapReduce programs, and also how to debug them. For this project, I also had to write numerous Spark utility functions, my favorite one being a sampling based Volume Estimation Algorithm for Spark dataframes which accurately predicts the data size (with 99\% precision) before materializing the dataframe to HDFS. Previously, I worked on a MapReduce based lifecycle management tool for retention of 6000+ datasets produced in our platform (Gobblin/MapReduce jobs that read user retention overrides or apply the default retention policies). 
</p>

<p align="justify">
Apart from this I am an active interviewer at LinkedIn, conducting interviews on 2 modules of Algorithms and 3 modules Infrastructure design. I am also a member of the Data Relevance Interview revamp committee, working on creating and reviewing new problems on Distributed Computing Algorithm design (problems involving Spark or MapReduce to solve large scale data challenges) and Machine Learning system design (problems involving designing large scale Machine learning and Recommender systems).
</p>

<p align="justify">
My research at CMU was on optimizing the performance of <a href="http://www.andrew.cmu.edu/user/gaurij/Research.html" target="_blank">Large-scale Machine Learning systems</a>, where training is performed by running stochastic gradient descent in a distributed fashion (using a central parameter server and multiple learner servers). In such systems, synchronization delays due to straggling learners can significantly increase the run-time of the training job. We are working on new algorithms that try to mitigate straggler effects in Synchronous SGD, whilst keeping a decent gradient quality and convergence time. We are also working on algorithms to reduce communication overhead in Distributed Synchronous SGD. </p>

<p align="justify">
In Summer 2017, I was a Software Engineering intern with LinkedIn's <a href="https://engineering.linkedin.com/teams/data" target="_blank">Data team </a>, where I wrote a data tooling library in Scala for query translation from Hive to Spark. To test my library, I prepared an optimized workflow (after tuning various Spark metrics) for Metrics Computation on LinkedIn's Ads data pipeline.
</p>