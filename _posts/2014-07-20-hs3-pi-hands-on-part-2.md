---
title: HS3-Pi hands-on (part 2)
author: iHomeAutomate
excerpt: 'The road to having remote (plugin) connections enabled on the HS3-Pi'
layout: article
permalink: /2014/07/20/hs3-pi-hands-on-part-2/
categories:
  - homeseer
tags:
  - homeseer
  - homeseer3
  - hs3
  - hs3-pi
  - raspberry_pi
  - z-wave
  - csharp
image:
  teaser: 2014/07/raspberry_400x250.jpg
ads: true
comments: true  
---
Here is a summary of my findings after I&#8217;ve been reading up on [HS3-Pi][1] and installed it on my spare Raspberry Pi. Note that the HS3-Pi is exactly the same HomeSeer build as running on the Zee. So we can assume that all below is applicable for the HomeSeer HomeTroller Zee hardware too.

**EXE plugin support?**
  
> Originally, we wanted the Zee to run EXE plugins just like the Windows HS3. However, there was a problem with MONO ver 2.10 where remote calls were not reliable and it would sometimes call the wrong function. So to fix this we made a minor change to the plugin API so plugins could be a DLL instead. This fixed the problem and we released the Zee with this special build of HS3. That is what the Zee build is today. Also, MONO only worked on the soft float version of Linux so that is what we had to use.
> <br/> &#8211; [Source][2]

**That was then, this is now: still no EXE plugin support?**
  
> Now, MONO is at version 3.2 on the PI, the PI OS is now hard float (means it runs a little faster) and the original remote call issue is fixed, so EXE plugins now work. Our intent was to change the Zee so it would support exe plugins. However, after much testing we decided to not do this. The reason is that each EXE plugin runs in its own MONO process and each process uses at least 30MB of memory. Add that to the mem that the plugin uses and you quickly start using up the 512MB of memory on the PI. So while it works ok with 2 or 3 plugins, it will probably run out of memory with more. So the user experience will less than optimal! So we decided to keep with the DLL plugins for now. I wish they would do a 1GB version of the PI, that would solve the problem.
> <br/>&#8211; [Source][2]

**Acceptable arguments, what about running the plugins remotely?**
  
> I have not actually tried that, but there is nothing in the code to stop it from working, so I think it should work. In fact, if you run an EXE plugin on the Zee from the HS3 folder, I think that also works. 
> <br/>&#8211; [Source][2]

Ok, let&#8217;s try running an EXE plugin from the HS3 folder on the HS3-Pi.


{% highlight bash %}
homeseer@HomeTrollerZEE /usr/local/HomeSeer $ sudo mono HSPI_MyZeePlugin.exe 

Unhandled Exception:
System.TypeLoadException: Could not load type 'HSPI_MyZeePlugin.HSPI' from assembly 'HSPI_MyZeePlugin, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null'.
[ERROR] FATAL UNHANDLED EXCEPTION: System.TypeLoadException: Could not load type 'HSPI_MyZeePlugin.HSPI' from assembly 'HSPI_MyZeePlugin, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null'.

{% endhighlight %}

**What&#8217;s with the System.TypeLoadException?**
  
> I did try remote plugins with the standard Zee and it does not work. The issue is that there is a slight plugin API change and that causes and exception to be thrown. So for now, the solution is to just run the full Linux version, that does support remote plugins.  
> &#8211; [Source][3]

**Switching to the full Linux version is too easy. Let&#8217;s try to connect remotely&#8230;**

{% highlight bash %}
System.Net.Sockets.SocketException: Invalid arguments
  at System.Net.Sockets.Socket.SetSocketOption (SocketOptionLevel optionLevel, SocketOptionName optionName, Int32 optionValue) [0x0003f] in /Volumes/build-root-ramdisk/mono-3.4.0/mcs/class/System/System.Net.Sockets/Socket_2_1.cs:1453 
  at System.Net.Sockets.Socket.set_NoDelay (Boolean value) [0x0002d] in /Volumes/build-root-ramdisk/mono-3.4.0/mcs/class/System/System.Net.Sockets/Socket_2_1.cs:1020 
  at HSCF.Communication.Scs.Client.Tcp.ScsTcpClient.CreateCommunicationChannel () [0x00000] in &lt;filename unknown>:0 
  at HSCF.Communication.Scs.Client.ScsClientBase.Connect () [0x00000] in &lt;filename unknown>:0 
  at HSCF.Communication.ScsServices.Client.ScsServiceClient`1[HomeSeerAPI.IHSApplication].Connect () [0x00000] in &lt;filename unknown>:0 
{% endhighlight %}

No luck. Let&#8217;s try to solve the System.TypeLoadException and run it locally on the HS3-Pi:

{% highlight bash %}
[ERROR] FATAL UNHANDLED EXCEPTION: System.IO.IOException: Not connected
  at System.Net.Sockets.NetworkStream..ctor (System.Net.Sockets.Socket socket, FileAccess access, Boolean ownsSocket) [0x00000] in &lt;filename unknown>:0 
  at System.Net.Sockets.NetworkStream..ctor (System.Net.Sockets.Socket socket) [0x00000] in &lt;filename unknown>:0 
  at (wrapper remoting-invoke-with-check) System.Net.Sockets.NetworkStream:.ctor (System.Net.Sockets.Socket)
  at HSCF.Communication.Scs.Communication.Channels.Tcp.TcpCommunicationChannel..ctor (System.Net.Sockets.Socket clientSocket) [0x00000] in &lt;filename unknown>:0 
  at HSCF.Communication.Scs.Client.Tcp.ScsTcpClient.CreateCommunicationChannel () [0x00000] in &lt;filename unknown>:0 
  at HSCF.Communication.Scs.Client.ScsClientBase.Connect () [0x00000] in &lt;filename unknown>:0 
  at HSCF.Communication.ScsServices.Client.ScsServiceClient`1[HomeSeerAPI.IHSApplication].Connect () [0x00000] in &lt;filename unknown>:0
{% endhighlight %}

It looks like nothing is listening on the default plugin-API port (10400). I should have checked that earlier!

{% highlight bash %}
homeseer@HomeTrollerZEE /usr/local/HomeSeer $ netstat --listen
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State      
tcp        0      0 *:ssh                   *:*                     LISTEN     
tcp        0      0 *:10401                 *:*                     LISTEN     
tcp        0      0 *:16683                 *:*                     LISTEN     
tcp        0      0 *:http                  *:*                     LISTEN     
{% endhighlight %}

Well, having read how the [homeseer communication framework][4] actually works, it&#8217;s time to get our hands dirty with a little Zee plugin to enable remote plugin connections. 

A little teaser :  
<img src="{{site.url}}/images/2014/07/hs-zee-plugin-remote-connections-1024x338.png" alt="hs-zee-plugin-remote-connections" width="900" height="297" class="aligncenter size-large wp-image-1453" />

To be continued.

 [1]: http://board.homeseer.com/showthread.php?t=169252
 [2]: http://board.homeseer.com/showpost.php?p=1129979&postcount=53
 [3]: http://board.homeseer.com/showpost.php?p=1130131&postcount=64
 [4]: {{site.url}}/2014/01/25/hscf-homeseer-communication-framework/
