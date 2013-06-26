---
layout: page
title: "Recent blogs"
description: ""
category: 
tags: []
---
{% include JB/setup %}
{% for post in site.posts %}
<a href="{{ root_url }}{{ post.url }}">
{{ post.title}}
<br>
</a>
{% endfor %}
