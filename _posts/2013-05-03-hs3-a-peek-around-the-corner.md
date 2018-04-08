---
title: 'HS3 &#8211; a peek around the corner'
author: iHomeAutomate
excerpt: 'A peek around the corner of HS3 (beta) release status'
layout: article
permalink: /2013/05/03/hs3-a-peek-around-the-corner/
categories:
  - homeseer
tags:
  - homeseer
  - homeseer3
  - hs3
  - road_to_hs3
disqus_identifier: "829 http://www.ihomeautomate.eu/?p=829"
comments: false
ads: true
image:
  teaser: 2013/05/Teaser-Events-1-400x250.jpg
  feature: road_to_hs3_1024x256.jpg
---
**2013, February 4** &#8211; About Z-Wave
  
> we have completely rewritten much of Z-Wave in HS3  
[Source][1]

**2013, February 21** &#8211; About SSL support
  
> &#8230; will SSL be supported in HS3? Yes this is planned.  
[Source][2]

**2013, February 26** &#8211; About the Z-Wave rework
  
> &#8230; In HS3, since our Z-Wave support is being vastly reworked, we have the opportunity to enhance this feature. For one thing, devices found on the Z-Wave Alliance certification list may be able to be identified by the software so that you, the consumer, will know whether you are using a device that has passed the Z-Wave Alliance&#8217;s tests of interoperability. What we will also be able to do is to identify a device by its product name, so that not only does it make sense looking at it in your own system, but it will also be able to be identified more easily as working with the current version of the Z-Wave plug-in for HS3 before you make a purchase.  
&#8230;.  
[Source][3]

**2013, March 10** &#8211; Status update
  
> We are in final stages of in-house testing, no beta this week, but any time now. As soon we work out reported issues we will move to posting a beta.  
[Source][4]

**2013, March 15** &#8211; Another status update
  
> In the middle of HS3 at the moment, trying to get a beta out.  
[Source][5]

**2013, April 8** &#8211; About new features
  
> It is almost easier to say what has not changed. Scripting support is still there, but probably most scripts will have to be touched in some way to update them to work with HS3 properly. For example, the device address is no longer the primary way of accessing a device &#8211; you can have a device without an address in fact, and you can have a device with an address that includes something specific about the device followed by the old code format if you want. For example, if your Z-Wave network is AABBCCDD, then you will have devices with a full address of AABBCCDD-10-Q05, which is a node 10 child device of network AABBCCDD. The code-only part of the address is Q05, which many people are familiar with. Accessing a device by name is unchanged.  
Plug-ins can now run on remote systems and you can run multiple instances of a plug-in. A big part of the delay has been due in part to us removing Z-Wave from the core program and making it a standalone plug-in, and the new features that are being put into that.  
It is our hope that testing of that plug-in will resolve some of the last of the more serious issues so that we can begin a public beta period soon.  
I wish I could spend all day telling you about it, as there are many things I left out, but please understand that we are working as hard as we can to bring this to you as soon as possible.  
[Source][6]

**2013, April 26** &#8211; About Perl scripting
  
> Perl will work on Windows, but not on Linux right now. I realize Linux supports perl but we are using a Windows scripting host to run the process. You can launch a perl script from HS but I am not sure how it can access the scripting API.  
The problem is that the scripting in windows is hosted using Windows Scritping Host, and this exposes our API to the script engine. This is not available on Linux, but I will research and see if there is a way to interface to Perl or Python from our application.  
[Source][7]

**2013, May 2** &#8211; A HS3 teaser
  
> A taste of things to come. Hang in there&#8230; won&#8217;t be too long before we can roll out the details for the first beta.  
[<img src="{{site.url}}/images/2013/05/Teaser-Events-1-300x245.jpg" alt="" title="Teaser-Events-1" width="300" height="245" class="aligncenter size-medium wp-image-837" />][8]
<br/>[HS3 Teaser (events)][9]

[Pictures & quotes coming from board.homeseer.com]

 [1]: http://board.homeseer.com/showpost.php?p=1053135&postcount=19
 [2]: http://board.homeseer.com/showpost.php?p=1055211&postcount=5
 [3]: http://board.homeseer.com/showpost.php?p=1055703&postcount=1
 [4]: http://board.homeseer.com/showpost.php?p=1057358&postcount=86
 [5]: http://board.homeseer.com/showpost.php?p=1057952&postcount=11
 [6]: http://board.homeseer.com/showpost.php?p=1060760&postcount=109
 [7]: http://board.homeseer.com/showpost.php?p=1062818&postcount=7
 [8]: {{site.url}}/images/2013/05/Teaser-Events-1.jpg
 [9]: http://board.homeseer.com/showpost.php?p=1063370&postcount=1
