---
title: HomeSeer Communication Framework
author: iHomeAutomate
excerpt: 'Want to know more about the HS Communication Framework ?'
layout: article
permalink: /2014/01/25/hscf-homeseer-communication-framework/
categories:
  - homeseer
tags:
  - dotnet
  - csharp
  - homeseer
  - homeseer3
  - hs3
image:
  teaser: 2014/02/building-blocks-400x250.jpg
ads: true
comments: false
---
One of the big changes in HS3 is its communication framework. HS3 introduced `HSCF.dll`, from the HS3 SDK documentation:

> &#8220;Plug-in&#8217;s communicate with HomeSeer through a simple TCP connection on port 10400. A communication framework called HSCF is used for 2-way communications and the connection remains open as long as the plug-in is connected. If a connection is lost, HomeSeer will attempt to re-connect with the plug- in. The communication framework also does its best to maintain the connection. This framework was chosen over Windows WCF due to its high performance, simplicity, and better compatibility with Linux.&#8221;

Wanting to know more on the framework I stumbled upon Tinks post on the [homeseer board][1]:

> &#8220;Yes, we created a framework for HS3 based upon a 3rd party product and turned it into the HSCF library that we use.  
> There are a lot of technical reasons why WCF would not work, reflection and uni-directionality being part of it, this framework eliminates a lot of those issues.&#8221;

Basically what we need to do to get connected to HS3 is:

{% highlight csharp %}
using System;
using HSCF.Communication.Scs.Communication.EndPoints.Tcp;
using HSCF.Communication.ScsServices.Client;
using HomeSeerAPI;
 
namespace HomeSeerClientApp
{
    class Program
    {
        static void Main()
        {
            ScsTcpEndPoint endpoint = new ScsTcpEndPoint ("127.0.0.1", 10400);
            IScsServiceClient<IHSApplication> client = ScsServiceClientBuilder.CreateClient<IHSApplication>(endpoint);
            client.Connect();
            
            // ...
            
            client.Disconnect();
        }
    }
}
{% endhighlight %}


Ok &#8211; that looks oddly similar to:

{% highlight csharp %}
using System;
using Hik.Communication.Scs.Client;
using Hik.Communication.Scs.Communication.EndPoints.Tcp;
using Hik.Communication.Scs.Communication.Messages;
 
/* Check out full source @ https://github.com/hikalkan/scs/blob/master/samples/SimpleMessaging/ClientApp/Program.cs */
 
namespace ClientApp
{
    class Program
    {
        static void Main()
        {
            var client = ScsClientFactory.CreateClient(new ScsTcpEndPoint("127.0.0.1", 10085));
            client.Connect(); //Connect to the server
            
            // ...
            
            client.Disconnect(); //Close connection to server
        }
    }
}
{% endhighlight %}

So, it looks like we found the [&#8220;3rd party product&#8221;][2] Tink refers to on the [homeseer board][1].  
I couldn&#8217;t find any license delivered with the HS3 binaries, nor could I find any reference to the original product. So giving the original framework author some credit, here are some references:

  * [SCS API][3]
  * [Usage of SCS][4]
  * [Implementation of SCS][5]
  * [SCS source on GitHub][2]
  * [SCS author on twitter][6]
  * [SCS author homepage][7]

 [1]: http://board.homeseer.com/showpost.php?p=1086996&postcount=10
 [2]: https://github.com/hikalkan/scs
 [3]: http://www.nudoq.org/#!/Packages/SCS
 [4]: http://www.codeproject.com/Articles/153938/A-Complete-TCP-Server-Client-Communication-and-RMI
 [5]: http://www.codeproject.com/Articles/155282/A-Complete-TCP-Server-Client-Communication-and-RMI
 [6]: https://twitter.com/hibrahimkalkan
 [7]: www.halilibrahimkalkan.com
