---
title: Projects
excerpt: "A collection of homemade projects we want to share"
author: iHomeAutomate
layout: archive
ads: true
---

<div class="tiles">
{% for post in site.categories.projects %}
    {% include post-grid.html %}
{% endfor %}
</div><!-- /.tiles -->
