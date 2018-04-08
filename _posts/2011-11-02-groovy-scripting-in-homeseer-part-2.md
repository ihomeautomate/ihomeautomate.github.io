---
title: Groovy scripting in HomeSeer (part 2)
author: iHomeAutomate
excerpt: 'HomeSeer plugin to write Groovy scripts and let them to the hard work connecting to your devices in homeseer.'
layout: article
permalink: /2011/11/02/groovy-scripting-in-homeseer-part-2/
categories:
  - homeseer
tags:
  - groovy
  - homeseer_plugin
  - script
  - java
image:
  teaser: 2011/09/homeseer.groovy.400x250.jpg
  feature: 2011/09/homeseer.groovy.1025x256.jpg
comments: false
ads: true  
disqus_identifier: "351 http://www.ihomeautomate.eu/?p=351"
---
In [part 1][1] we just used groovy standalone to connect to HomeSeer, now we take a step up to improve performance :-).

I finally found time to write about the HomeSeer Groovy Script Server and the HSGroovyScript HomeSeer Plugin. I took me a while before I got all the HomeSeer API functions working from within Groovy, reason: DLL hell and x64/x86 COM component compatibility problems :-).

Basically we have a (standalone) Groovy Server running waiting for commands/scripts to run. This server can run on any (windows) machine, and connects remotely to the HomeSeer host using the HS speakerclient active-x components. A plugin for HomeSeer then does the necessary work to start a groovy script on the applicable machine. Unfortunately I couldn&#8217;t find a way to initiate the script other than by an event. I tried fiddling with the scripting possibilities within HomeSeer itself, but failed to get a `.groovy` in there. If you guys have another idea, feel free to let me know.

When initializing, the server connects to the HomeSeer host, and prepares the `homeseer2.application` COM component and its `Scheduler.hsapplication` reference. These 2 objects are injected in each script/command executed as variables `hsi` and `hs`.  
This means that the scripts don&#8217;t have to initiate the connection to HomeSeer every time.

Example:

{% highlight groovy %}
hs.writeLog("MyGroovyScript", "This is written remotely powered by a iHomeAutomate.com HomeSeer Groovy script!")

def version = hs.version()
def uptime = hs.systemUpTime()
hs.speak "Your HomeSeer machine is running version ${version} and is already up for ${uptime}."
{% endhighlight %}

Result looks like this:  
![hs.groovy.server.script.in.action]({{ site.url }}/images/2011/11/hs.groovy.server.script.in_.action.png)

Or we could do some more complicated stuff:

{% highlight groovy %}
def deviceEnumerator = hs.getDeviceEnumerator()

while (!deviceEnumerator.finished()) {
    def device = deviceEnumerator.getNext()
    def type = device.dev_type_string
    def deviceCode = device.hc + device.dc

    if (type.toLowerCase().contains("battery")
            &#038;&#038; hs.deviceValue(deviceCode) &lt; 75) {
                hs.writeLog "Battery low detected for device ${device.name}"
    }
}
{% endhighlight %}

On HomeSeer side, the scripts are fired by events:  
![hs.event.groovyscript.run]({{ site.url }}/images/2011/11/hs.event_.groovyscript.run_.png)

The result looks like:  
![groovy.script.executing]({{ site.url }}/images/2011/11/groovy.script.executing.png)

If people would be interested in this homeseer plugin, feel free to comment below. Of course opinions and other comments are welcome too :-).

 [1]: {{site.url}}/2011/09/07/groovy-scripting-groovy-scripts-from-in-homeseer/ "Groovy Scripting in HomeSeer (part 1)"
 [2]: http://www.ihomeautomate.eu/wp-content/uploads/2011/11/hs.groovy.server.script.in_.action.png
 [3]: http://www.ihomeautomate.eu/wp-content/uploads/2011/11/hs.event_.groovyscript.run_.png
 [4]: http://www.ihomeautomate.eu/wp-content/uploads/2011/11/groovy.script.executing.png
