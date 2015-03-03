---
title: 'Continuing the HS3 gossip&#8230;'
author: iHomeAutomate
excerpt: "Read what's new in HS3..."
layout: article
permalink: /2011/12/03/continuing-on-the-hs3-gossip/
dsq_thread_id:
  - 492374557
categories:
  - homeseer3
tags:
  - homeseer
  - homeseer3
  - hs3
  - road_to_hs3
image:
  teaser: HomeSeer.Appetizer.400x250.jpg
  feature: road_to_hs3_1024x256.jpg
disqus_identifier: "543 http://www.ihomeautomate.eu/?p=543"
comments: true
ads: true
---
Last month, [Rich &#8220;rjh&#8221;][1] over at [HomeSeer][2] has revealed some nifty information regarding the upcoming HomeSeer 3. 

In case anyone wants to re-read, here is the previous [HS3 gossip & chatter][3].

**Let&#8217;s not talk *release date* :-), let&#8217;s talk *beta version*&#8230;**

> As for a ship date, whatever I post will be wrong, so I won&#8217;t post one I will say we hope to have a beta around the end of the year, or Jan time frame. But do not hold me to that! 

**Let&#8217;s talk *changes*&#8230;**
  
> We have totally re-written the event engine, which has proven to be a big job. This includes a totally new interface (web page) for creating events. It is much easier to use and more robust then before. New additions include counters and timers as well as better grouping of events.
  
* The status page is totally new (the old one is still there but is now considered a utility page for device maintenance) The new page auto updates device status, allows for floor plan views, and an edit mode for editing the view on the web page.  
* We are using jquery for the web pages, and if you are familiar with this, you know how powerful it is. The web pages look and act more like an application than a web page, with dialogs and dynamic updates. Plugins will have access to jquery but they don&#8217;t need to know how it works or write any javascript.  
* The &#8220;button bar&#8221; has been replaced with a jquery menu to allow for better navigation of the web interface.  

**Let&#8217;s talk *linux*&#8230;**  

> One big change is Linux compatibility. The entire application runs under Windows or Linux so you can choose the OS and hardware you want to run it on.  

**Let&#8217;s talk *plugin-compatibility***  

> Since there are changes to the plugin API, we hope to have a test version for plugin authors asap, so they can make any necessary changes. We have major changes we want to make the plugin API, but we are holding them offer for a later release. The first release will have a plugin API similar to HS2 so that most plugins will work with either little or no modifications. Almost every plugin will need some modification if they want to be compatible with the Linux version.  

[Source][4]

 [1]: http://board.homeseer.com/member.php?u=37857
 [2]: http://board.homeseer.com/
 [3]: {{site.url}}/2011/10/11/homeseer-3-gossips-and-appetizers/
 [4]: http://board.homeseer.com/showpost.php?p=992874&postcount=18
