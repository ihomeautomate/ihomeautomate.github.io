---
title: 'HomeSeerToy in C#'
author: iHomeAutomate
excerpt: 'Some tips and tricks to connect from a C# application to HomeSeer'
layout: article
permalink: /2010/04/24/homeseertoy-in-csharp/
comments: true
ads: true
image:
  feature: 2010/05/HomeSeerToy.png
  teaser: 2010/05/HomeSeerToy-400x250.jpg
disqus_identifier: '76 http://smart-living.geoblog.be/?p=76'
categories:
  - homeseer 
tags:
  - homeseer
  - dotnet
  - csharp
---
I felt the need to control my lights with the media-player remote-control I had available. I assumed it would be easy to quickly build a C# console application which I could easily start from within EventGhost. 

The application was finished rather fast, EventGhost was quickly configured, yet the result was not behaving fast enough to my taste. EventGhost needed to start the external console application, which connects to HomeSeer and triggers an event. The delay was too annoying. I decided to make a bit harder: let&#8217;s build a plugin for EventGhost, which connects to HomeSeer. Some of the C# quotes however, I decided to share:

Requisites:

  * HomeSeer &#8211; <a title="HomeSeer" href="http://www.homeseer.com/" target="_blank">http://www.homeseer.com/</a> (to actually control the lights)
  * HomeSeer Speaker Client &#8211; <a title="HomeSeer Download Page" href="http://www.homeseer.com/downloads/index.htm" target="_blank">http://www.homeseer.com/downloads/index.htm</a> (only needed in case you want to access HomeSeer from a remote machine)
  * Visual Studio Express &#8211; <http://www.microsoft.com/express/Windows/> (when no other alternative at hand)

References to `Scheduler.dll` and `HomeSeer2.dll` should reveal the necessary classes and namespaces to control HomeSeer.

{% highlight csharp %}
private static HomeSeer2.application hsapp = new HomeSeer2.application();
private static Scheduler.hsapplication hs = new Scheduler.hsapplication();
{% endhighlight %}

Connect to HomeSeer, I assume the port is actually optional:

{% highlight csharp %}
hsapp.SetHost(args[0] + ":" + args[1]);
hsapp.Connect(args[2],  args[3]);
hs = hsapp.GetHSRef();
{% endhighlight %}

Detailed device information is available via the device code as parameter.

{% highlight csharp %}
int deviceRef = hs.GetDeviceRef(args[4]);
DeviceClass device = hs.GetDeviceByRef(deviceRef);

Console.WriteLine("Sending command " + args[5] + " to device " + device.Name);
{% endhighlight %}

Sending a command isn't hard either. I did notice the command parameter to be case sensitive: "On" seem to work, "on" did not.

{% highlight csharp %}
if (hs.IsOn(args[4]))
{
     Console.WriteLine("Device is currently On, switching Off");
     hs.ExecX10(args[4], "Off", 0, 0, false);
}
else
{
     Console.WriteLine("Device is currently Off, switching On");
     hs.ExecX10(args[4], "On", 0, 0, false);
}
{% endhighlight %}

References:

  * [http://www.homeseer.com/support/homeseer/WebHelp/scripting/homeseer\_scripting\_interface\_(function\_quick_reference).htm][1]
  * [http://www.homeseer.com/support/homeseer/WebHelp2/tipstricks/tipstricks\_controlling\_homeseer_remotely.h][2]

 [1]: http://www.homeseer.com/support/homeseer/WebHelp/scripting/homeseer_scripting_interface_(function_quick_reference).htm
 [2]: http://www.homeseer.com/support/homeseer/WebHelp2/tipstricks/tipstricks_controlling_homeseer_remotely.htm
