---
layout: page
title: Blog
permalink: /blog/
---

A repository of reviews of the research papers I found interesting. A lot of reviews are dated (2018) and reflected my views when I was still at CMU. However thanks to a year of working with some of the smartest minds of Data systems at LinkedIn, I now have a new found perspective on how to think about systems at scale. I plan to re-review some of the major ones, and also add reviews to some new papers I have been reading (mostly on large scale data and machine learning systems). This blog also contains our technical discussions from Mountain View CS Reading Group.s
<br>

<ul class="listing">
{% for post in site.posts %}
  {% capture y %}{{post.date | date:"%Y"}}{% endcapture %}
  {% if year != y %}
    {% assign year = y %}
    <li class="listing-seperator">{{ y }}</li>
  {% endif %}
  <li class="listing-item">
    <time datetime="{{ post.date | date:"%Y-%m-%d" }}">{{ post.date | date:"%Y-%m-%d" }}</time>
    <a href="{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a>
  </li>
{% endfor %}
</ul>
