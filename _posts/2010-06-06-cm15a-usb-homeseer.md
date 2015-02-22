---
title: CM15A USB / Homeseer
author: iHomeAutomate
excerpt: 'An overview of what is needed to get the CM15A X10 USB to work with HomeSeer'
layout: article
permalink: /2010/06/06/cm15a-usb-homeseer/
image:
  - http://smart-living.geoblog.be/wp-content/uploads/2010/06/CM15A_homeseer-300x108.jpg
dsq_thread_id:
  - 404660285
categories:
  - homeseer
tags:
  - cm15a
  - homeseer
  - usb
  - x10
ads: true
disqus_identifier: '101 http://smart-living.geoblog.be/?p=101'
comments: true
---
Some people are wondering what exactly needs to be installed to get the CM15A working with HomeSeer. Here you'll find a short summary of how I did it on my Windows XP HomeSeer machine.

Requisites:

  1. CM15A USB (Hardware)
  2. CM15A USB Wireless Remote Drivers
  3. HomeSeer &#8211; <a title="HomeSeer" href="http://www.homeseer.com/" target="_blank">http://www.homeseer.com/</a>
  4. HomeSeer CM15A USB plugin

Let's get to work! Trying to follow what the plugin subscribes:

> Download and install the free ActiveHome CM15A SDK from X10.com, this may fix any issue you are seeing. Make sure you install the CM15A USB drivers before installing this plugin.

> <cite>Source: HomeSeer plugin page, *CM15A X10 USB*</cite>

The full version of ActiveHome, delivered with the CM15A, was of no use at all. I did try to do a quick search for the SDK, but could not find a valid download anywhere. I settled for the drivers only, with success.
{: .notice}

  1. Download &#8220;X10 USB Wireless Remote Drivers&#8221;, found at [X10 Downloads](http://www.x10.com/support/support_soft1.htm){:target="_blank"}.
  2. Install drivers (run the executable)
  3. Installer asks for a restart, so let&#8217;s reboot.
  4. Plug in the CM15A (USB)
  5. Plug in power of the CM15A
  6. Windows will recognize the CM15A

So far the Windows part, let's continue with the HomeSeer part.

![CM15A Homeseer Plugin]({{ site.url }}/images/2010/06/CM15A_homeseer-300x108.jpg)

  1. Start Homeseer
  2. Search for the &#8220;CM15A X10 USB&#8221; plugin on the updater page. Currently version 1.0.0.6.
  3. Select the plugin and install
  4. Restart HomeSeer after plugin download notification
  5. HomeSeer will start the CM15A X10 installer automatically, just click &#8220;Next&#8221; a few times. Finish up with &#8220;Close&#8221;.
  6. Installer will ask to enable the plugin automatically when starting HomeSeer. Make your choice.

When done, the Setup / Plug-in interfaces page shows the CM15A X10 plugin, status &#8220;Enabled&#8221;. Finally, you&#8217;ll be able to add your X10 devices!
