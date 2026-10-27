---
title: HomeSeer changelog
layout: single
permalink: /homeseer/changelog/
---

All weekly HomeSeer changelogs, newest first. Back to [All about HomeSeer](/homeseer/).

<ul>
{% for post in site.tags['homeseer_changelog'] %}
  <li>{{ post.date | date: "%B %d, %Y" }} &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
{% endfor %}
</ul>
