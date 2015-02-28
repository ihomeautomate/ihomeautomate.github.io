---
title: Groovy scripting in HomeSeer (part 1)
author: iHomeAutomate
excerpt: 'Feel the need to explore the bounderies of HomeSeer scripting? Try to connect to HomeSeer with Groovy, an agile dynamic language for the Java Platform.'
layout: article
permalink: /2011/09/07/groovy-scripting-groovy-scripts-from-in-homeseer/
categories:
  - homeseer
tags:
  - groovy
  - homeseer
  - java
  - script
image:
  teaser: 2011/09/homeseer.groovy.400x250.jpg
  feature: 2011/09/homeseer.groovy.1025x256.jpg
comments: true
ads: true
---
I felt like fooling around with <a href="http://groovy-lang.org/" target="_blank">Groovy</a> and [HomeSeer][1], so I started investigating what the options are. Of course you can just run a command-line groovy script from within HomeSeer, that&#8217;s not a challenge. The challenge was to let the groovy script actually connect to HomeSeer. 

Requisites:

  1. HomeSeer &#8211; <a title="HomeSeer" href="http://www.homeseer.com/" target="_blank">http://www.homeseer.com/</a>
  2. HomeSeer Speaker Client &#8211; <a title="HomeSeer Download Page" href="http://www.homeseer.com/downloads/index.htm" target="_blank">http://www.homeseer.com/downloads/index.htm</a> (only needed in case you want to access HomeSeer from a remote machine)
  3. Groovy &#8211; <a title="Groovy" href="http://groovy-lang.org/documentation.html#gettingstarted" target="_blank">Getting started with Groovy</a>
  4. Scriptom &#8211; [Scriptom Groovy Module][2]

If you know your way around the HomeSeer functions, it should be rather easy. Before we can connect, let&#8217;s initialize our Active-X component, using scriptom. Make sure that the groovy classloader can actually find the scriptom classes!

{% highlight groovy %}
// importing the necessary scriptom classes
// make sure the scriptom libraries are available on classpath (eg. put them inside the .groovy/lib folder)
import org.codehaus.groovy.scriptom.ActiveXObject

def hsi = new ActiveXObject("HomeSeer2.application")
def hs = null

// configuration to connect to the homeseer host
def host = "localhost"
def user = "default"
def password = "default"
{% endhighlight %}

Next, we try to connect&#8230;

{% highlight groovy %}// Let's try to connect
println "Connecting to HomeSeer host..." 
hsi.setHost host
def ret = hsi.connect(user, password)

if (ret?.trim().length() &gt; 0) {
	println "Error: $ret"
} else {
	println "Connection successful."
}
{% endhighlight %}

Then we try to do something with our hs object :). As example I just log a message, print out the uptime and version of the host, and perform a speak action.

{% highlight groovy %}
hs = hsi.getHSRef()
hs?.writeLog("GroovyScript", "Connection successful")
println "You should see a GroovyScript log message showing in the HomeSeer console.\n"

def version = hs?.version()
def uptime = hs?.systemUpTime()
println "The HomeSeer host has version $version installed and is running for $uptime\n"
hs?.speak "Hello HomeSeer from Groovy! Powered by a www.iHomeAutomate.eu Groovy script!"
{% endhighlight %}

Let&#8217;s not forget to disconnect again

{% highlight groovy %}println "Disconnecting..."
hsi.disconnect()
{% endhighlight %}

This is the result:  
![Hello HomeSeer from Groovy]({{ site.url }}/images/2011/09/helloHomeseerFromGroovy-1.png)

![Hello HomeSeer from Groovy]({{ site.url }}/images/2011/09/helloHomeseerFromGroovy-2.png)

The downside of starting a (command line) script like this from homeseer is that we always need to initialize a connection to homeseer. In a next part, coming up later, I&#8217;ll create a plugin for HomeSeer executing groovy scripts at runtime, making the groovy scripts a lot faster. 

Here is the full HelloHomeSeerFromGroovy script as gist:
{% gist 8ef8fd8960021f812943 %}

 [1]: http://www.homeseer.com/
 [2]: http://groovy.codehaus.org/COM+Scripting "Scriptom Groovy Module"
 [3]: http://www.ihomeautomate.eu/wp-content/uploads/2011/09/helloHomeseerFromGroovy-1.png
 [4]: http://www.ihomeautomate.eu/wp-content/uploads/2011/09/helloHomeSeerFromGroovy-2.png
 [5]: http://www.ihomeautomate.eu/wp-content/uploads/2011/09/HelloHomeSeerFromGroovy-www.iHomeAutomate.eu_.zip
