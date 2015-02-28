---
title: Everspring AN158 powermeter facts
author: iHomeAutomate
excerpt: 'Introduction to the Everspring AN158 device and its power metering features'
layout: article
permalink: /2011/09/06/everspring-an158-powermeter-facts/
disqus_identifier: '293 http://www.ihomeautomate.eu/?p=293'
categories:
  - z-wave
tags:
  - an158
  - everspring
  - homeseer
  - powermeter
  - z-wave
comments: true
ads: true
image:
  teaser: an158-400x250.jpg
---
The Everspring AN158 device is a Z-Wave on/off plug with power metering capabilities. It reports both the actual consumption (in Watts) and the accumulated usage (in KWh). The device is rated IP20, hence only for indoor dry environments.

#####Include in z-wave network  
When no nodeid is assigned to the device, meaning it hasn&#8217;t been included in a z-wave network yet, the led is blinking: 2 seconds on, 2 seconds off. To enter inclusion mode (or exclusion mode when AN158 was already included), press On/Off button three times within 1.5 seconds.  
If you need to reset the device, press On/Off button three times within 1.5 seconds and within 1 second keep the On/Off button pressed for 5 seconds until the led goes off.

##### Something to look out for  
When *important* devices are hooked up to the AN158, watch our for power failures :). Apparently the AN158 does not switch automatically to its previous state. In my case it was connected to a freezer; luckily I remembered to manually switch the AN158 on after power was restored.

##### HomeSeer  
I remember having difficulties getting the AN158 device to show up in HomeSeer. After playing around for a while, I upgraded HomeSeer to version 2.5.0.23 (latest available version at that time). After that it was dead-easy, I now have 4 devices for each AN158:

  * Root device (for configuration)
  * Switch device (On/Off)
  * Watts consumed
  * Accumulated consumption (kW Hours)

##### Configuration  
By default the AN158 will report the power usage every 300 seconds. We can configure this to a lower interval in HomeSeer (or other).

  * Go to the AN158 root device
  * Choose settings
  * Select parameter number 3 (default is set to 30 for 300 seconds)
  * Change to the desired number (eg. 1 for 10 seconds interval time)

##### Socket types  
Don't worry, you&#8217;ll find the AN158 you need for the socket in your region

  * AN158-2 (Germany/Netherlands)
  * AN158-3 (UK)
  * AN158-4 (Italy)
  * AN158-5 (Denmark)
  * AN158-6 (Belgium/France)

##### Power Metering .plan  
I originally planned on hooking all my power meter devices to Google Power Meter (using a homemade HomeSeer plugin). However, since Google Power Meter is discontinued, I need either a (free) alternative or build something myself. Feel free to let me know what good alternatives there are.
