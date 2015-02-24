---
title: Python scripts in HomeSeer
author: iHomeAutomate
excerpt: 'Howto describing how to get those python scripts running in HomeSeer'
layout: article
permalink: /2010/06/17/python-scripts-in-homeseer/
image:
  teaser: python-400x250.png
categories:
  - homeseer
tags:
  - homeseer
  - python
ads: true
comments: true  
---
For a while I was searching an alternative to VBScript as script language within HomeSeer. I almost decided to go for C# and buying the [Script Connector Plugin](http://store.homeseer.com/store/Script-Connector-Plug-In-P460C155.aspx), but decided to try an out-of-box solution first. Python was first on my list.

1. Be sure to install the correct Python package: <a title="ActivePython" href="http://www.activestate.com/activepython/downloads" target="_blank">ActiveState ActivePython</a>. The Community Edition (free) will do just fine.
2. I found out - the hard way - that not any ActivePython version seemed to work with HomeSeer. I downloaded and installed version 2.6.(5.12) first, but I could not get beyond the `Running script, cannot add script engines`. I uninstalled version 2.6 and downloaded the older 2.5.(5.7) version, which worked just fine.
3. No need to restart Windows, or even HomeSeer.
4. Add a script with extension .py to HomeSeer and try it.

Here's the script I used for my first tests:

{% highlight python %}
def Main():
  hs.WriteLog("Debug","Hello HomeSeer from Smart-Living in Python!")
{% endhighlight %}        
