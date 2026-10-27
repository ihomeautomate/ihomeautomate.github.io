---
title: All about HomeSeer
layout: single
permalink: /homeseer/
toc: true
---

## iHomeAutomate tools and plugins

### HomeTroller Zee/HS-Pi

* [HSPI_EnableRemotePlugins](/2014/08/28/enable_remote_plugins_homeseer_zee_hs3pi/)

### iHomeAutomate development utilities

* [HomeSeer lazybones templates](https://github.com/ihomeautomate/homeseer-lazybones-templates)
* [Gradle HomeSeer plugin](https://github.com/ihomeautomate/gradle-homeseer-plugin)

## Road to HS3

A compilation of chatter and rumours about HS3 from 2009 until 2013:

{% for post in site.tags['road_to_hs3'] %}
* [{{ post.title }}]({{ post.url }})
{% endfor %}

## HomeSeer articles

{% assign count = 0 %}
{% for post in site.categories['homeseer'] %}
{% unless post.tags contains 'homeseer_changelog' %}
{% if count < 12 %}
{% assign count = count | plus: 1 %}
* [{{ post.title }}]({{ post.url }})
{% endif %}
{% endunless %}
{% endfor %}

## HomeSeer changelog

<ul>
{% assign count = 0 %}
{% for post in site.tags['homeseer_changelog'] %}
  {% if count < 5 %}
    {% assign count = count | plus: 1 %}
  <li>{{ post.date | date: "%B %d, %Y" }} &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endif %}
{% endfor %}
  <li><a href="/homeseer/changelog/">More changelogs</a></li>
</ul>
