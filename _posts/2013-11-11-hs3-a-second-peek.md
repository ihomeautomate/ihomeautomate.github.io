---
title: HS3, a second peek
author: iHomeAutomate
layout: article
permalink: /2013/11/11/hs3-a-second-peek/
categories:
  - homeseer
tags:
  - homeseer
  - homeseer3
  - hs3
  - road_to_hs3  
image:
  teaser: /2013/11/second-chance-400x250.jpg
  feature: road_to_hs3_1024x256.jpg
comments: true
ads: true  
---
HS3, the (beta) linux binaries are released, so I immediately fiddled with it on my mac <img src="http://www.ihomeautomate.eu/wp-includes/images/smilies/icon_smile.gif" alt=":-)" class="wp-smiley" />

{% highlight bash %}
ihomeautomate$ sudo ./go  

Unhandled Exception:
System.TypeLoadException: A type load exception has occurred.
[ERROR] FATAL UNHANDLED EXCEPTION: System.TypeLoadException: A type load exception has occurred.
{% endhighlight %}

I guess I needed to upgrade mono, the version I had was :

{% highlight bash %}
ihomeautomate$ mono --version
Mono JIT compiler version 2.10.12 (mono-2-10/c9b270d Thu Mar  7 21:38:12 EST 2013)
Copyright (C) 2002-2012 Novell, Inc, Xamarin, Inc and Contributors. www.mono-project.com
	TLS:           normal
	SIGSEGV:       normal
	Notification:  kqueue
	Architecture:  x86
	Disabled:      none
	Misc:          softdebug 
	LLVM:          yes(2.9svn-mono)
	GC:            Included Boehm (with typed GC)
{% endhighlight %}

After upgrading:

{% highlight bash %}ihomeautomate$ mono --version
Mono JIT compiler version 3.2.3 ((no/8d3b4b7 Mon Sep 16 23:46:28 EDT 2013)
Copyright (C) 2002-2012 Novell, Inc, Xamarin Inc and Contributors. www.mono-project.com
	TLS:           normal
	SIGSEGV:       altstack
	Notification:  kqueue
	Architecture:  x86
	Disabled:      none
	Misc:          softdebug 
	LLVM:          yes(3.3svn-mono)
	GC:            sgen
{% endhighlight %}

{% highlight bash %}ihomeautomate$ sudo ./go
HomeSeer Linux starting...
11/11/2013 3:41:50 PM:[Logging]->Result of the attempted creation of a new log database: Log Database Created.
11/11/2013 3:41:50 PM:[Startup]->Loading Settings
11/11/2013 3:41:50 PM:[Startup]->Settings Loaded.
11/11/2013 3:41:50 PM:[Startup]->Current sunrise/sunset values calculated.
11/11/2013 3:41:50 PM:[Startup]-> 
11/11/2013 3:41:50 PM:[Startup]->********************************************************************************
11/11/2013 3:41:50 PM:[Startup]->            HomeSeer version 3.0.0.42 Edition: HS3 Pro Starting Now
11/11/2013 3:41:50 PM:[Startup]->********************************************************************************
11/11/2013 3:41:50 PM:[Startup]-> 
...
{% endhighlight %}

Bingo! Now let&#8217;s play <img src="http://www.ihomeautomate.eu/wp-includes/images/smilies/icon_smile.gif" alt=":-)" class="wp-smiley" />  
Although it does start up correctly, it looks like we are missing a text-to-speech utility for osx. Not sure if anyone is capable to free up some time to compile the osx binary for <a href="http://www.speech.cs.cmu.edu/flite/" title="flite" target="_blank">flite</a>? <img src="http://www.ihomeautomate.eu/wp-includes/images/smilies/icon_smile.gif" alt=":-)" class="wp-smiley" />

{% highlight bash %}11/11/2013 8:24:23 PM:[TTS]->Speak ():Welcome to Home-Seer
./speak.sh: line 2: flite: command not found
{% endhighlight %}

Next I was looking like crazy to enable HSTouch (Lite), and found it to be disabled in the updater file for OS&#8217;s other than Windows. Obviously not visible in the homeseer web interface :-(.  
So, why not force it by copying HSPI_HSTOUCH.exe from a windows machine :-).

{% highlight bash %}11/12/2013 7:55:00 PM:[Startup]->Checking for available plug-ins
11/12/2013 7:55:00 PM:[Plug-In]->Found plug-in: HSTouch Server, version: 3.0.0.11
{% endhighlight %}

However, when enabling it:

{% highlight bash %}11/12/2013 7:55:24 PM:[HSTouch Server]->Server started on port 10200
Invalid type A.c6dd698c8b2eb6a7b6f5e1c223905bd9b for instance field A.c8ca4444aa67e6a34abece120adc7d915:c19690ea0732a2f261e332e863f8e8b47
11/12/2013 7:55:24 PM:[Error]->Initializing plug-in(2): HSTouch Server Instance::A type load exception has occurred.0STACK:  at System.Runtime.Remoting.Proxies.RealProxy.PrivateInvoke (System.Runtime.Remoting.Proxies.RealProxy rp, IMessage msg, System.Exception&#038; exc, System.Object[]&#038; out_args) [0x00000] in &lt;filename unknown>:0 
11/12/2013 7:55:24 PM:[Plug-In]->Finished initializing plug-in HSTouch Server
{% endhighlight %}

Source:

  * <a title="HS3 linux installation" href="http://forums.homeseer.com/showthread.php?t=162813" target="_blank">HS3 Linux Installation</a> 
  * <a title="HS3 Linux build 3.0.0.42" href="http://forums.homeseer.com/showthread.php?t=162814" target="_blank">HS3 Linux build 3.0.0.42</a>
