---
title: My first week with Vera
author: iHomeAutomate
excerpt: 'A first experience with my MiOS Vera V3 Z-Wave Home Control Box'
layout: article
permalink: /2012/03/19/my-first-week-with-vera/
disqus_identifier: "716 http://www.ihomeautomate.eu/?p=716"
categories:
  - vera
tags:
  - luup
  - vera
  - z-wave
comments: true
ads: true
image:
  teaser: 2012/03/vera_melu_400x250.png
---
I finally decided to introduce <a href="http://micasaverde.com/vera-3.php" title="Vera V3" target="_blank">Vera (V3)</a> to my home. This is what I learned the first week.

##### Installing ntp client
Eventhough I&#8217;ve setup my location (city and timezone) correctly in the UI, it never showed the correct time. I tried reloading and restarting a few times, nothing seemed to work. I finally decided to do some (minor) &#8220;power-using&#8221; and logged on with ssh to install an ntp-client. Using putty I could easily log in with the root user (using password mentioned on the back of my Vera), and install an ntp client:

[<img src="{{site.url}}/images/2012/03/vera3.ntp_.png" alt="" title="vera3.ntp" width="664" height="259" class="aligncenter size-full wp-image-717" />][1]  
Problem resolved :-)

##### Advanced network configuration
I&#8217;m using Vera as a wifi router in my local network and I needed some advanced configuration(s) done. I expected this to be available somewhere in UI5, but found nothing. Catching up on Vera forum threads, it looks like in UI4 there was a &#8220;Advanced configuration&#8221; link on the &#8220;Net & wifi&#8221; page. In UI5, that came with Vera V3 out of the box, this has been removed.  
Ignoring that pain and knowing that Vera basically just runs on top of an <a href="https://openwrt.org/" target="_blank">OpenWRT</a>, you can just browse to openwrt [web management console][2] using `http://your\_vera\_ip/cgi-bin/webif/info.sh` (use your root user and password to login).

##### Adding z-wave device to Vera
Before moving my full z-wave network to Vera (I currently have HomeSeer as primary controller), I planned to introduce non critical devices first. I had a Everspring AN158 device lying around, destined to be my first test unit. I expected it to be &#8220;plug and play&#8221;, but that wasn&#8217;t the case:  
My spare AN158 did not want to auto-configure correctly with Vera. On/Off however, did work correctly immediately after including, the power metering features of the AN158 did not. Within the Vera UI5, the device always ended up red with the warning &#8220;failed at: purging associations&#8221;. Resetting the AN158, including/excluding multiple times, desperately playing around with parameter values didn&#8217;t help. Logging on with ssh and snooping around in some log files, I saw many z-wave communication timeouts. Bringing my AN158 even closer to Vera (cm range) did not help :-).

I than decided to try to include another Everspring AN158 device, which I first needed to exclude from my Homeseer z-wave network. This second AN158 device *automagically* configured correctly immediately: all features of the device working. Trying a few more times with the first AN158, still no luck.

Eventually, (more than) 48 hours later, it showed up green in Vera. Vera finally caught up with the device configuration and all features are now working as expected.

##### Fooling around with Vera&#8217;s apps functionality  
As a &#8220;power user&#8221; :-), I wanted to setup some virtual devices. Using Apps/develop apps/create device, I added a motion sensor:

{% highlight json %}
DeviceType: urn:schemas-micasaverde-com:device:MotionSensor:1  
DeviceFile:D_MotionSensor1.xml
{% endhighlight %}
 
    
    
The newly created device did not behave as a motion sensor (it did not have arm/bypass buttons) and it did not show up under &#8220;sensors&#8221;. Playing around with its configuration never fixed it. Eventually I ended up doing a luup reload&#8230;

{% highlight javascript %}
luup.call_action("urn:micasaverde-com:serviceId:HomeAutomationGateway1","Reload",{},0)
{% endhighlight %}
    
&#8230; after which I finally had a proper (virtual) motion sensor. I&#8217;m not sure if this behaviour is the same for all device types.

 [1]: {{site.url}}/images/2012/03/vera3.ntp_.png
 [2]: https://dev.openwrt.org/browser/branches/whiterussian/openwrt/package/webif/files/www/cgi-bin/webif/info.sh
