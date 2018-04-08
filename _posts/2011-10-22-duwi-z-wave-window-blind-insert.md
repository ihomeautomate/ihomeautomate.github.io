---
title: Duwi z-wave window blind Insert
author: iHomeAutomate
excerpt: "A while back I've encountered some issues customizing the Duwi blind control. I've taken some notes and decided to share with the rest of the world."
layout: article
permalink: /2011/10/22/duwi-z-wave-window-blind-insert/
dsq_thread_id:
  - 450683248
categories:
  - z-wave
tags:
  - duwi
  - homeseer
  - popp
  - vera
  - z-wave
image:
  teaser: 2011/10/duwi.ihomeautomate.blinds-400x250.jpg
comments: false
ads: true  
---
A short summary of some of the notes I had available for those who want to figure out how to customize the Duwi sun blind control.

###### Customizing the operating times (using the blind control) 

Please note a shutter/window blind does not necessarily have identical operating times in the UP and DOWN directions. The window blind control has to be adjusted to this, so that a desired, preset value (e.g. window blind to 80%) is attained both in the upward as well as downward motion.
Also note that you (possibly) have to remove the mounted rocker of the window blind for this programming step.
The window blind must ﬁrst be driven along the upward direction up to the end stop. The reduction of the operating time must be started from the upper maximum position, if not the programmed values would be falsiﬁed.
{: .notice}
  
> <cite>Source: Duwi manual</cite>
  
1. Move the window blind along the upward direction up to the end stop
2. Simultaneously press the “UP” and “DOWN” buttons of the window blind for 2 seconds, the LED blinks green.
3. Move the window blind with the “UP” or “DOWN” buttons of the window blind in the intended direction. During this measurement time, the LED promptly blinks green.
4. Release control in the target position. The window blind stops, the LED conﬁrms the successful folding with a 3 second green light and a failed folding with a red light.

![operating.times.duwi.blind.de]({{ site.url }}/images/2011/10/operating.times_.duwi_.blind_.de_.png)
 
###### Customizing the operating times (using parameter 0 with third party software &#8211; for experienced users only!)
 

Warning: the adjustment of the operating times should be undertaken only by well-versed technicians.
{: .notice-warning}
        
> <cite>Source: Duwi manual</cite>

Send parameter 0 to the blind control root device node with 2 bytes HEX value(s) (one UP, one DOWN):

* 0x00 = no interruption/permanent operation
* 0x01-0x7F = 1 second to 127 seconds in 1-second steps
* 0x80-0xFE = 130 seconds (0x80) to 1390 seconds (0xFE) in 10 second-steps
* 0xFF = factory settings 120 seconds
        
Examples:

* Parameter 0, value 0xFFFF should reset it to factory settings (120 seconds for both UP and DOWN).
* Parameter 0, value 0x7878 sets it to 120 seconds (for both UP and DOWN)
        
![duwi.parameters.blind.de]({{ site.url }}/images/2011/10/duwi.parameters.blind_.de_.png)        
                
I don&#8217;t have any Vera available to verify, but it should be the similar to HomeSeer, possibly even easier. With HomeSeer, parameter 0 should be sent as a decimal value, for example for 0x7878 send decimal value 30840 (120 seconds for both UP and DOWN).
It&#8217;s been a while since I verified this, but if my earlier notes are correct, this is how I parametrized the operating times of my blinds. So definitely handle with care! The preferred way of customizing the operating times is still using the control itself :-). 
          
###### Adjusting the stop functionality (using the blind control)

> <cite>Source: Duwi manual</cite>

Apparently you can also program the shutter actuator in a way that, in case of a press in the opposite direction, the shutter won‘t stop, but continues immediately in the opposite direction. I haven&#8217;t verified myself, but the manual states the following: 
            
* Hold the “UP” and “DOWN” button of the shutter actuator simulaneously for 5 seconds. Please note, the device should not be included in any network (yet)!

###### Adjusting the stop functionality (using parameter 1 with third party software &#8211;)

Warning: for experienced users only
{: .notice-warning}

> <cite>Source: Duwi manual</cite>

The manual states the following:<br /> 

* Send configuration command parameter 1 to the root node with the value “0” in order to *disable* the stop-functionality.
* Send configuration command parameter 1 to the root node with the value “1” in order to *enable* the stop-functionality.

![duwi.parameters.blind.de]({{ site.url }}/images/2011/10/homeseer.duwi_.blind_.parameter.1.configuration.png)

I have verified this with HomeSeer and it seems to work. Again, handle with care!

> <cite>Source: different <a title="Duwi sun blind manual" href="http://www.duewi.de/index.php?productid=37344">manuals </a>in different languages.</cite>
