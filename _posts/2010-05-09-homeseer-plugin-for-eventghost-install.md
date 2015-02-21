---
title: Installation HomeSeer plugin for EventGhost
author: iHomeAutomate
excerpt: 'Describing how to install the EventGhost plugin to interface with HomeSeer'
layout: article
permalink: /2010/05/09/homeseer-plugin-for-eventghost-install/
image:
  - http://ihomeautomate.com/wp-content/uploads/2010/05/addplugin.jpg
categories:
  - EventGhost
tags:
  - eventghost
  - homeseer
  - python
ads: true
---
Some people have contacted me to explain in a few words how exactly to install the EventGhost HomeSeer plugin. This will hopefully do just that.

I assume that the basic features of EventGhost are known, if not please refer to the [EventGhost Short Manual](http://www.eventghost.org/docs/short_manual/index.html){:target="_blank"}.

1. Install HomeSeer Speaker Client if you are planning to call HomeSeer from a remote machine
2. [Download](https://github.com/ihomeautomate/eventghost-hs-plugin/releases){:target="_blank"} the latest version of the plugin
3. Copy the folder `Homeseer` to the `/plugins` folder inside the installation directory of EventGhost
4. Start EventGhost
5. Add Plugin `HomeSeer`. It'll be available in the `Other` list 
<br/>![Add HomeSeer Plugin voor Event Ghost]({{ site.url }}/images/2010/05/addplugin-300x166.jpg)
6. The new plugin will then be available in the Autostart section. 
<br/>![Autostart]({{ site.url }}/images/2010/05/autostart.jpg)
7. Add the HomeSeer hostname and user credentials to the plugin configuration.
<br/>![Configuration]({{ site.url }}/images/2010/05/configuration-300x213.jpg)
<br/>Don't forget to save the configuration! An incorrect configuration will be displayed in the EventGhost log window.
![cannotconnect]({{ site.url }}/images/2010/05/cannotconnect.jpg)
8. Add Action, not many actions available, only the ones that were applicable to my situation.<br/>
![addactions]({{ site.url }}/images/2010/05/addactions.jpg)
   * Action Configuration<br/>This is how the speak action configuration looks:
![homeseer-speak]({{ site.url }}/images/2010/05/configure.speak_-300x213.jpg)
   * The device code is needed for the OnOffCommand configuration.
   ![OnOffCommandAction]({{ site.url }}/images/2010/05/OnOffCommandAction-300x213.jpg)
   * Test :-). You can find the `Test` button on the Action configuration window. <br/>
When testing the Speak Action, this will show in the EventGhost log:
<br/>![speak-test]({{ site.url }}/images/2010/05/speaktest-300x42.jpg)<br/>
In your HomeSeer log, the result is also visible:
![speak-homeseerlog]({{ site.url }}/images/2010/05/speak-homeseerlog-300x15.jpg)<br/>
The OnOffCommand action will switch the configured device to either On/Off, depending on its current status. E.g. when the configured device is &#8220;On&#8221;, it&#8217;ll switch to &#8220;Off&#8221;. In my situation this was all I need to be able to bind one button to one specific device.
