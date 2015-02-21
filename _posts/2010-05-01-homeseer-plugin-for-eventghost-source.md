---
title: Source Homeseer plugin for EventGhost
author: iHomeAutomate
excerpt: 'A HomeSeer plugin for EventGhost'
layout: article
permalink: /2010/05/01/homeseer-plugin-for-eventghost-source/
image:
  - http://ihomeautomate.com/images/hellohomeseer.jpg
disqus_identifier: '4 http://smart-living.geoblog.be/?p=4'
comments: true
ads: true
categories:
  - EventGhost
tags:
  - eventghost
  - homeseer
  - python
---
For quite a while now I make use of <a title="EventGhost" href="http://www.eventghost.org/" target="_blank">EventGhost</a> to control <a title="MediaPortal" href="http://www.team-mediaportal.com/" target="_blank">MediaPortal</a> with my remote-control. Why shouldn&#8217;t I make use of the same remote to execute <a title="HomeSeer" href="http://www.homeseer.com/" target="_blank">HomeSeer </a>events? 

Unfortunately there wasn&#8217;t any existing plugin for EventGhost doing this. That&#8217;s why I tried to quickly build something in C# ([see here]({% post_url 2010-04-24-homeseertoy-in-csharp %})). However, the result wasn&#8217;t what I expected it to be, so I decided to create an EventGhost (Python) plugin myself; I must admit, Python was completely new to me.

Requisites:

  * EventGhost &#8211; <a title="EventGhost" href="http://www.eventghost.org/" target="_blank">http://www.eventghost.org/</a> (to trigger the events)
  * HomeSeer &#8211; <a title="HomeSeer" href="http://www.homeseer.com/" target="_blank">http://www.homeseer.com/</a> (to control the devices)
  * HomeSeer Speaker Client &#8211; <a title="HomeSeer Download Page" href="http://www.homeseer.com/downloads/index.htm" target="_blank">http://www.homeseer.com/downloads/index.htm</a>

<img class="aligncenter" title="Hello HomeSeer!" src="http://www.ihomeautomate.eu/images/hellohomeseer.jpg" alt="" width="435" height="259" />

When EventGhost is installed on the same machine running HomeSeer, nothing extra needs to be installed. However, when a remote machine is used to control HomeSeer, then you'll need to download and install the HomeSeer Speaker Client. As such, you can call the necessary HomeSeer COM objects from Python.

The source for the plugin is a .py file, which needs to be copied into `/plugins/Homeseer` located in the `EventGhost` folder.

Necessary imports to use the COM objects:

{% highlight python %}
import win32com.client
{% endhighlight %}

We create a simple Homeseer class to call the HomeSeer functions:

{% highlight python %}
class Homeseer():
    hsi = win32com.client.Dispatch("HomeSeer2.application")
    hs = win32com.client.Dispatch("Scheduler.hsapplication")

    ...

    def connect(self):
        print "Trying to connect to Homeseer-host " + self.hostname + " using user " + self.username + "."
        self.hsi.SetHost(self.hostname)
        rval = self.hsi.Connect(self.username, self.password)
        if rval == "":
            print "Successfully connected to Homeseer " + self.hostname + " using user " + self.username + "."
            self.connected = True
        else:
            print "Error: " + rval
            self.hsi.Disconnect()
            self.connected = False

        if self.connected:
            self.hs = self.hsi.GetHSRef

    def disconnect(self):
        if self.connected:
            self.hsi.Disconnect()
            print "Disconnected from Homeseer."
            self.connected = False
{% endhighlight %}        

A hs.speak test function is added to easily test our setup:

{% highlight python %}
def doSpeak(self, speech):
        if self.connected:
            print "Speaking " + speech
            self.hs.speak(speech)
        else:
            print "Not connected to Homeseer."
{% endhighlight %}

The actual function that, depending on the status of a device, sends a On or Off command to HomeSeer:

{% highlight python %}
def doOnOffCommand(self, deviceCode):
        if self.connected:
            if self.hs.IsOn(deviceCode):
                command = "Off"
            else:
                command = "On"

            print "Sending command " + command + " to " + deviceCode
            self.hs.ExecX10(deviceCode, command, 0, 0, False);

        else:
            print "Not connected to Homeseer."
{% endhighlight %}

The actual EventGhost plugin which will call the HomeSeer class:

{% highlight python %}
class HomeseerPlugin(eg.PluginBase):

    ...

    def __start__(self, hostname, username, password):
        global HOMESEERINSTANCE
        HOMESEERINSTANCE = Homeseer(hostname, username, password)
        HOMESEERINSTANCE.connect()

    def __stop__(self):
        HOMESEERINSTANCE.disconnect()  

    ...
{% endhighlight %}

The actual EventGhost Actions which will call HomeSeer commands:

{% highlight python %}
class OnOffCommand(eg.ActionBase):

    def __call__(self, deviceCode):
        HOMESEERINSTANCE.doOnOffCommand(deviceCode)
    ...

class Speak(eg.ActionBase):

    def __call__(self, speech):
        HOMESEERINSTANCE.doSpeak(speech)
    ...
{% endhighlight %}


Download the full source code [here](https://github.com/ihomeautomate/eventghost-hs-plugin/releases){:target="_blank"}.

References:

  * <http://www.eventghost.org/docs/scripting.html>
  * [http://www.homeseer.com/support/homeseer/WebHelp/scripting/homeseer\_scripting\_interface\_(function\_quick_reference).htm][1]
  * [http://www.homeseer.com/support/homeseer/WebHelp2/tipstricks/tipstricks\_controlling\_homeseer_remotely.h][2]

 [1]: http://www.homeseer.com/support/homeseer/WebHelp/scripting/homeseer_scripting_interface_(function_quick_reference).htm
 [2]: http://www.homeseer.com/support/homeseer/WebHelp2/tipstricks/tipstricks_controlling_homeseer_remotely.htm
