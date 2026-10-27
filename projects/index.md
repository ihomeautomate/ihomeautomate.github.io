---
title: Projects
layout: single
permalink: /projects/
---

A collection of homemade projects we want to share.

{% for post in site.categories.projects %}
* [{{ post.title }}]({{ post.url }}) — {{ post.excerpt | strip_html | truncate: 100 }}
{% endfor %}
