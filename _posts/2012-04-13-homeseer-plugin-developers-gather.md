---
title: Homeseer plugin developers gather!
author: iHomeAutomate
excerpt: 'Homeseer 3 changes for plugin developers'
layout: article
permalink: /2012/04/13/homeseer-plugin-developers-gather/
categories:
  - homeseer
tags:
  - dotnet
  - csharp
  - homeseer
  - hs2
  - hs3
  - mono
image:
  teaser: HomeSeer.Appetizer.400x250.jpg
  feature: road_to_hs3_1024x256.jpg
---
[Rich &#8220;rjh&#8221;][1] over at [HomeSeer][2] has posted a [survey][3] for plugin developers revealing some nifty (technical) information regarding the upcoming HomeSeer 3. 

**API functions removed from HS3**
{% highlight csharp %}
AddAction  
AddCondtion  
CAPIHandleStatus  
ClearConditions  
ClearLastX10  
ControlThermostat  
DeviceStatus  
DialInternetConnection  
DisconnectInternetConnection  
ExecX10ByName  
ExecX10NoLog  
ExecX10 // CAPI interface should be used instead  
GetEventEnumerator  
GetEvent // replaced with GetEventEx  
GetTVGTData  
lastx10  
NewCondition  
NewEventAction  
NewEventEx  
NewEventGetRef  
PrintOut  
PrintOutRaw  
RunningAsService  
SetDeviceLastChange  
SetDeviceStatus  
SetDeviceStatusByName  
X10InterfaceStatus  
{% endhighlight %}

> (more details on the survey page)  

**Device control / Device status functions removed?**
  
> All you need to do is add a device value pair that matches your old status (like ON=1, Off=0), and you have your old device status. Devices now use value pairs for all status and we have a new editor where you can edit the pairs as well as the graphics assigned to all values. It is a lot cleaner. If you worked with CAPI in HS2, this is the new API for device control and device status.

**COM support**  

> Support for COM is removed, so no COM based plugins will work (HS 1.7 plugins).

**Linux support**
  
> Linux support is accomplished under MONO, so as long as your plugin is pure .NET, it should work under MONO on Linux. Make sure you install all of MONO, including the VisualBasic.Compatibility dll. 

> To check your plugin, just load into the [MOMA][4] application and it will tell you which functions are not supported. Getting [MOMA][4] to clear your plugin is a good first step to getting Linux compatible. (MOMA runs under Windows so Linux is not needed). You can ignore the late binding errors as they should not be a problem.  

**Scripts**
  
> Currently, VBScript still works in HS3 (Windows only) and I may leave it in for now, maybe only for a while and then remove it later. The scripting API will have changes though so many scripts will still need to be modified. Also, VBScript&#8217;s won&#8217;t work at all on Linux so the downside of leaving it there is confusion for the user. Any VB.NET scripts are supported on the Linux platform.

**UI**
  
> ASP.NET is still supported (and supported on Linux). Old classic asp will not be supported since it will not work on Linux (it relied on the VBScript engine). We do have new API&#8217;s for building web pages that include a robust collection of screen elements that are Jquery based. This allows for dynamic HTML5 web pages.

[Source thread][5]  
[HS3 survey sticky thread][3]  
[HS3 survey for plugin developers][6]  
[HS3 development FAQ][7]

Feel free to re-read some of the [previous HS3 buzz][8].

 [1]: http://board.homeseer.com/member.php?u=37857
 [2]: http://board.homeseer.com/
 [3]: http://board.homeseer.com/showthread.php?t=153642
 [4]: http://www.mono-project.com/MoMA
 [5]: http://board.homeseer.com/showthread.php?t=153633
 [6]: http://kwiksurveys.com/online-survey.php?surveyID=LLMDMN_9e0526df&u=hs3plugins
 [7]: http://board.homeseer.com/showthread.php?t=153646
 [8]: {{site.url}}/2012/03/23/awaiting-more-hs3-goodies/
