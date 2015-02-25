---
title: Y-Cam Knight first experience
author: iHomeAutomate
excerpt: 'My first experience with my Y-Cam Knight IP Camera'
layout: article
permalink: /2010/09/25/y-cam-knight-first-experience/
image:
  teaser: Ycam_logo-400x250.jpg
categories:
  - ip-camera
tags:
  - ip-camera
  - y-cam
comments: true
ads: true
---

Here's my first experience with the Y-Cam Knight IP Camera.

##### Quick start
I&#8217;ve unboxed the Y-Cam, read the &#8220;Quick Start&#8221; manual and immediately plugged in the network cable and power plugs. In my routers web console I found its IP and default hostname `knight`.  
Browsing to the ip, using the default username `admin` and password `1234`, gave me access to the video stream and settings page. Without installing additional software, only the browser of my choice, I could get everything to work quite fast.

##### Wireless  
The idea is to have the Y-Cam work on WiFi, so I&#8217;ve changed the wireless configuration to match my network settings. Soon I got the impression wasn't at all stable anymore: slow response times, even no response at all from time to time. After a few reboots (power off/on), I decided to disable UPNP, which worked much better already! Still, while playing with the settings there still were glitches of unresponsiveness. I hope when just using the video stream it&#8217;ll be a bit more stable.

##### Software  
The software that was included was quite useless. It gives you the ability to search for the camera (even if you don&#8217;t know the ip), after which you apply the correct configuration. What I did notice: when already configured and running in a wireless setup, the software doesn&#8217;t seem to find the camera.  
I also tried to use Multi-Live, another application included with the Y-Cam. It could not connect to my camera, no timeout, no error message, nothing. Luckily we can still use the browser!

##### Firmware  
My Y-Cam was delivered with version 3.25 of the firmware. The lastest available version is 3.39, so obviously I updated it. I followed the instructions: download new version, unzip, upload via the firmware upgrade feature using the browser, wait, wait some more and reboot. The first reboot it did not seem to connect automatically to my WIFI anymore. After a few other reboots we were back in business. The new firmware had give me a new option: Y-Cam hive, which I did not try yet.

##### Smart Phone  
I intend to use my smart-phone to watch the Y-Cam stream(s). In my case an Android 2.1 device. Looking for the &#8220;Y-Cam MultiLive&#8221; app in the Android Market showed me no results. An older Android 1.6 device did show me the correct app. So unfortunately, for now, no Android app!

##### Tools  
There is a feature to upload a snapshot to an ftp server periodically. Sending out a snapshot by email is also possible. The FTP option I did not try yet, the email feature I did. Unfortunately even with the correct SMTP configuration it did not seem to work. Still need to look into it in more detail. Worst case I can solve this doing my own (HomeSeer) automation.

##### Colors  
The colors don&#8217;t seem to feel naturally, especially the purple glow. This appears to be normal behaviour, caused by the IR leds. The nightly snapshots look much better obviously!
