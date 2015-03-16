---
layout: article
title: "Tag Index"
modified:
excerpt: "An archive of posts organized by tag."
share: false  
ads: true
---

### An archive of posts sorted by tag name.

<ul class="tag-box">
{% assign tags_list = site.tags | sort %}  
  {% for tag in tags_list %} 
    {% for data_tag in site.data.tags %}
      {% if data_tag.slug == tag[0] %}
        <li><a href="{{ site.url }}/tag/{{ tag[0] | replace:' ','-' | downcase }}/">{{ data_tag.name | downcase }} <span>{{ tag[1].size }}</span></a></li>
      {% endif %}
    {% endfor %}
    
  {% endfor %}
</ul>

