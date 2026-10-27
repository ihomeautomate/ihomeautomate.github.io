---
layout: splash
title: "iHomeAutomate"
header:
  overlay_image: /images/home-1600x800.jpg
  overlay_filter: 0.4
  overlay_color: "#000"
tagline: "Tips and information about home automation"
---

<div class="feature__wrapper">
{% for post in site.posts %}
  {% if post.tags contains 'homeseer_changelog' %}
  {% elsif post.categories contains 'projects' %}
  {% else %}
    <div class="feature__item">
      <div class="archive__item">
        <div class="archive__item-teaser">
          <a href="{{ post.url }}">
            {% if post.header.teaser %}
              <img src="{{ post.header.teaser }}" alt="{{ post.title }}">
            {% else %}
              <img src="/images/home-400x250.png" alt="{{ post.title }}">
            {% endif %}
          </a>
        </div>
        <div class="archive__item-body">
          <h2 class="archive__item-title"><a href="{{ post.url }}">{{ post.title }}</a></h2>
          <p class="archive__item-excerpt">{{ post.excerpt | strip_html | truncate: 120 }}</p>
        </div>
      </div>
    </div>
  {% endif %}
{% endfor %}
</div>
