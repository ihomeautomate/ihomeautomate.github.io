---
title: All about HomeSeer
author: iHomeAutomate
layout: article
ads: true
toc: true
---

## iHomeAutomate tools and plugins

### HomeTroller Zee/HS-Pi

  * [HSPI_EnableRemotePlugins][9] 

### iHomeAutomate development utilities

  * [HomeSeer lazybones templates][10] 
  * [Gradle HomeSeer plugin][11]
  
[1]: ftp://ftp.homeseer.com/pub/setuphs2_5_0_49.exe
[2]: ftp://ftp.homeseer.com/pub/HomeSeerUpdate2_5_0_81.exe
[3]: ftp://ftp.homeseer.com/pub/setuphspro2_5_0_49.exe
[4]: ftp://ftp.homeseer.com/pub/HomeSeerUpdateHSPRO2_5_0_81.exe
[5]: http://www.homeseer.com/updates3/SetupHS3_3_0_0_163.exe
[6]: http://www.homeseer.com/updates3/hslinux_zee_3_0_0_152.tar.gz
[7]: http://homeseer.com/updates3/SetupHS3_3_0_0_171.exe
[8]: http://www.homeseer.com/updates3/hslinux_hs3_3_0_0_163.tar.gz
[9]: {{site.url}}/2014/08/28/enable_remote_plugins_homeseer_zee_hs3pi/
[10]: https://github.com/ihomeautomate/homeseer-lazybones-templates
[11]: https://github.com/ihomeautomate/gradle-homeseer-plugin
[12]: {{site.url}}/tag/road_to_hs3
[13]: http://www.homeseer.com/updates3/hslinux_hs3_3_0_0_171.tar.gz
[14]: http://www.homeseer.com/updates3/hslinux_zee_3_0_0_171.tar.gz

## Road to HS3

We've prepared a compilation of chatter and rumours about HS3 from 2009 until 2013. Here is [the road to HS3][12]:

<div class="archive-wrap">
<ul class="th-grid"> 
 {% for post in site.tags['road_to_hs3'] %}
      <li><a href="{{ site.url }}{{ post.url }}" title="{{ post.title }}"><img src="{{ site.url }}/images/{{ post.image.teaser }}" alt=""></a></li>
 {% endfor %}
</ul>
</div><!-- /.archive-wrap -->

## HomeSeer articles

Interested in homemade HomeSeer plugins, hacks, information and tips, treats or tricks? Here are the latest articles in the <a href="{{site.url}}/category/homeseer">HomeSeer category</a>:

<div class="archive-wrap">
<ul class="th-grid">
   {% assign count = 0 %}
   {% if site.categories['homeseer'] %}
     {% for post in site.categories['homeseer'] %}
       {% if post.tags contains 'homeseer_changelog' %}
       {% else %}
         {% if count < 12 %}
           {% assign count = count|plus:1 %}
           <li><a href="{{ site.url }}{{ post.url }}" title="{{ post.title }}"><img src="{{ site.url }}/images/{{ post.image.teaser }}" alt=""></a></li>
         {% endif %}
       {% endif %}
     {% endfor %}
   {% endif %}
</ul>
</div><!-- /.archive-wrap -->
   
## Latest versions

Ever wondered what the latest HomeSeer version is? Lost track of your beta versions? You're not alone :-), below is a list we'll try to keep up to date.

### official releases

  * [HomeSeer HS2 2.5.0.49 (installer)][1] update to [HS2 2.5.0.81 (update)][2] (Windows)
  * [HomeSeer HS2PRO 2.5.0.49 (installer)][3] update to [HS2PRO 2.5.0.81 (update)][4] (Windows)
  * [HomeSeer HS3/HS3PRO 3.0.0.163 (installer)][5] (Windows)
  * [HomeSeer HS3 Zee 3.0.0.152][6] (HomeTroller Zee or HS3-Pi)
  * [HomeSeer HS3/HS3PRO 3.0.0.163][8] (Linux)

### beta

  * [HomeSeer HS3/HS3PRO 3.0.0.171 (installer)][7] (Windows) 
  * [HomeSeer HS3/HS3PRO 3.0.0.171][13] (Linux) 
  * [HomeSeer HS3 Zee 3.0.0.171][14] (HomeTroller Zee or HS3-Pi)    
   
## HomeSeer changelog

<ul> 
 {% assign count = 0 %}
 {% for post in site.tags['homeseer_changelog'] %}
  {% if count < 5 %}
      {% assign count = count|plus:1 %}
      {% include post-list.html %}
  {% endif %}
 {% endfor %}
 <li>
  <a href="{{site.url}}/tag/homeseer_changelog">More changelogs</a>
 </li>
</ul>
