---
layout: page
title: "Recent blogs"
description: ""
category: 
tags: []
---
{% include JB/setup %}
<ul>
  {% for post in site.posts %}
    <li>{{ post.date | date: "%Y-%m-%d" }} <a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
