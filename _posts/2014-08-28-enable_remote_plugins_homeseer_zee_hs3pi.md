---
title: Enable remote plugins on your HomeSeer Zee
author: iHomeAutomate
excerpt: 'Enable remote plugins on your HomeSeer Zee or HS3-Pi'
layout: article
permalink: /2014/08/28/enable_remote_plugins_homeseer_zee_hs3pi/
categories:
  - homeseer
tags:
  - csharp
  - homeseer
  - homeseer3
  - hs3
  - hs3-pi
comments: true
ads: true
image:
  teaser: 2014/08/remote-connections_400x250.png
---
I promised a way to connect your HomeSeer 3 plugins remotely to your HS3-Pi or HomeSeer HomeTroller Zee. Running through some hoops it has (partly) succeeded. You might want to read the previous posts on the [topic][1] before getting your hands dirty.

  * [HS3-Pi][2]
  * [HS3-Pi hands-on part 1][3]
  * [HS3-Pi hands-on part 2][4]

##### How it works

The current version of `hslinux_zee` (3.0.0.106) does not allow remote plugin connections, [the feature is basically disabled][4]. What the `HSPI_EnableRemotePlugins`-plugin does, is re-using the available out-of-box HomeSeer framework API to (re)enable it. The source-code is available on [github.com/ihomeautomate][5] under the [LGPL-2.1][6] license. Definitely check out its [readme][7]-page for the most up-to-date information.

##### Running through hoops

One might expect that invoking [HomeSeer Communication Framework][8] aka `HSCF` would be enough to achieve our goal.

{% highlight csharp %}
scsServiceApplication = ScsServiceBuilder.CreateService (new ScsTcpEndPoint ("127.0.0.1", PLUGIN_API_PORT));
scsServiceApplication.AddService<IHSApplication, hsapplication> (hsApplication);
scsServiceApplication.AddService<IAppCallbackAPI, clsHSPI> (appCallbackAPI);
{% endhighlight %}


&#8230; unfortunately it wasn&#8217;t. Somehow out-of-box HomeSeer code fails to get the remote plugin initialized. That&#8217;s where we&#8217;ve needed to disable some core functionality.

{% highlight csharp %}
appCallbackAPI.StopCheckTimer(); 
// It'll make sure the out-of-box plugin check is disabled for our custom initialization to be triggered.
{% endhighlight %}

&#8230; and replace it with our custom implementation, leveraging the available `appCallbackAPI`. This seems to do the trick. 

{% highlight csharp %}
for (int i = 0; i < appCallbackAPI.IOobjsPending.Count; i++) {
	clsHSPI.PluginHolder pluginHolder = (clsHSPI.PluginHolder)appCallbackAPI.IOobjsPending.GetByIndex (i);
					
	// ...
 
	HomeSeerAPI.IPlugInAPI clientProxy = pluginHolder.client.GetClientProxy<HomeSeerAPI.IPlugInAPI> ();
	pluginHolder.obj_ref = clientProxy; 
 
	hsApplication.WriteLog (PLUGIN_NAME, "'" + pluginHolder.obj_name + ":" + pluginHolder.InstanceName + "'.InitIO(" + pluginHolder.sPortNumber + ")");
	string text = clientProxy.InitIO (pluginHolder.sPortNumber);
 
	// ...
}{% endhighlight %}

##### Licensed plugins won&#8217;t work out-of-box

From [this thread][9] we understand that when using licensed remote plugins, there needs to be a copy located on the HomeSeer server. This is how HomeSeer checks the plugins `AccessLevel`. Unfortunately for us, `hslinux_zee` disables the scanning of HSPI_ .exe files in `/usr/local/HomeSeer`.

Our workaround &#8211; implementing our own scanning mechanism &#8211; won&#8217;t work with out-of-box licensed plugins. Invoking such `hs3_linux`-plugin through *reflection* fails due to conflicting HomeSeerAPI interface(s). Not much we can do about that, except asking the plugin author to recompile against the proper *hslinux_zee* DLL binaries and release a *hslinux_zee* version. In theory, when that is done, and, a copy of the .exe is located in `/usr/local/HomeSeer` of the HomeSeer server, the `HSPI_EnableRemotePlugins`-plugin *should* do the rest. This is un-tested, feel free to confirm my theory.

Good news however, for free plugins `AccessLevel == 1`, this all should work without having a copy on the HomeSeer server.

##### Get started

Grab the latest release available on [Bintray][10], copy it to `/usr/local/HomeSeer` on your HS3-Pi or HomeTroller Zee and restart. The plugin should then be visible in the *manage plugins* section, ready to be enabled. Please refer to the [readme on github][7] on how to proceed in detail.

In case you want to use the latest snapshot build, they should be available in [JFrogs OSS artifactory][11].

 [1]: {{site.url}}/tag/hs3-pi/
 [2]: {{site.url}}/2014/07/12/hs3pi
 [3]: {{site.url}}/2014/07/13/hs3-pi-hands-on-part-1
 [4]: {{site.url}}/2014/07/20/hs3-pi-hands-on-part-2
 [5]: https://github.com/ihomeautomate/HSPI_EnableRemotePlugins
 [6]: https://github.com/ihomeautomate/HSPI_EnableRemotePlugins/blob/master/LICENSE.txt
 [7]: https://github.com/ihomeautomate/HSPI_EnableRemotePlugins/blob/master/README.md
 [8]: {{site.url}}/2014/01/25/hscf-homeseer-communication-framework/
 [9]: http://forums.homeseer.com/showthread.php?t=169287
 [10]: https://bintray.com/ihomeautomate/HomeSeer/HSPI_EnableRemotePlugins
 [11]: http://oss.jfrog.org/artifactory/libs-snapshot/eu/ihomeautomate/homeseer/HSPI_EnableRemotePlugins/
