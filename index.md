---
layout: home
permalink: /
image:
  feature: home-1600x800.jpg
---


<div class="tiles">
{% assign count = 0 %}
{% for post in site.posts %}
  {% if post.tags contains 'homeseer_changelog' %}
  
  {% else %}
    {% if post.categories contains 'projects' %}
    {% else %}
      {% if count < 50 %}
        {% assign count = count|plus:1 %}
        {% include post-grid.html %}
      {% endif %}
    {% endif %}
  {% endif %}
{% endfor %}
</div><!-- /.tiles -->
