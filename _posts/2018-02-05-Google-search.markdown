---
layout: post
title:  "Combined reviews for 1. The Anatomy of a Large-Scale Hypertextual Web Search Engine, and 2. The PageRank Citation Ranking: Bringing Order to the Web"
date:   2018-02-05 08:00:00
author: Souptik Sen
---

## Summary
<p>
The first paper describes the foundations of the Google search engine. It takes us through the initial Google prototype and describes the challenges in scaling search engine to handle the massive web page repository of the Web. The 2nd paper deals with the implementation of PageRank, a method for rating Web pages using the link structure of the web. There are millions of unorganized heterogeneous web pages on the World Wide Web. This algorithm helps in determining which web page is important and relevant to the query made on the search engine.
</p>

## What I liked about this paper
<p>
a.  One of the key contributions of the Google founders is the PageRank- Larry and Sergey share their intuition that the link graph embedded in the web is a valuable resource for ranking the quality of web pages. This was a novel idea at that time, and probably one of those major intuitions that made Google a search engine leader.<br>
b.  The repository of HTML pages crawled acts as the source of truth for data, and all other data structures can be rebuilt from the repository when necessary. This implicit way of doing fault tolerance has probably been inspiration to fault tolerance in lambda architecture used for big data systems.<br>
Large scale data structures: The paper introduces some novel data structures to store and retrieve documents with as little cost as possible. Some notable ones include BigFiles, Hit lists and inverted indices.<br>
</p>

## Critical comments
<p>
a.  The Web search today is highly personalized according to your preferences. The 2nd paper does touch upon personalized pagerank but doesn't go into details.<br>
b.  Under "Results and Performance", the author's claim of " our own experience with Google has shown it to produce better results than the major commercial search engines for most searches" is not very convincing.<br>
c.  Paper doesn't talk about link farms which was widely used as a SEO technique in 2000s. Google Panda (2011) talks about this update which aimed to lower the rank of "low-quality sites" or "thin sites" in particular "content farms", and to return higher-quality sites near the top of the search results.<br>
</p>

## Questions
<p>
a.  How can we achieve personalized pagerank/ search?<br>
b.  Can the idea of pagerank be extended on social network graphs? To detect maybe spam profiles?<br>
c.  How do we test the search quality (accuracy/performance) of a search engine? Is there a standard performance metric like ImageNet in the case of image recognition tasks?<br>
</p>
