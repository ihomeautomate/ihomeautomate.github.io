---
title: HS3-Pi hands-on (part 1)
author: iHomeAutomate
excerpt: 'Get HomeSeer HS3-Pi installed on your Raspberry Pi'
layout: article
permalink: /2014/07/13/hs3-pi-hands-on-part-1/
categories:
  - homeseer
tags:
  - homeseer
  - hs3
  - hs3-pi
  - raspberry_pi
  - z-wave  
image:
  teaser: 2014/07/raspberry_400x250.jpg
ads: true
comments: true  
---
For OSX people, here&#8217;s a little guide to get the [HS3-Pi image][1] up and running on your Raspberry Pi. People running another OS please refer to the [HS3-Pi install guide][2].

Format the sd card in &#8216;Disk Utility&#8217; as msdos.  
Then open a terminal window and run the following:

<pre>diskutil list
</pre>

The output will have a &#8216;FDisk\_partition\_scheme&#8217; entry similar to: 

<pre>[...]
/dev/disk1
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:     FDisk_partition_scheme                        *8.0 GB     disk1
   1:                 DOS_FAT_32 UNTITLED                8.0 GB     disk1s1
</pre>

Find your sdcard, in the above example it&#8217;s disk1.  
Unzip the downloaded HS3-Pi image and place it somewhere accessible.  
Go back to &#8216;Disk Utility&#8217; and unmount (do not eject) the SD card partition.  
Then dd the image to the sd card using something like the following (NOTE: DD IS DANGEROUS, BE CAREFUL WHEN USING IT. MAKE SURE THE diskX MATCHES THE NUMBER ABOVE)

<pre>sudo dd if=/Users/aUserName/Downloads/HomeSeer-HS3Pi-Image of=/dev/disk1
</pre>

You may need to wait up to 10 minutes while it copies. There won&#8217;t be any progress indicator. You can interrupt dd with CTRL-C, and you&#8217;ll see something like:

<pre>6654737+0 records in
6654736+0 records out
3407224832 bytes transferred in 3131.851312 secs (1087927 bytes/sec)
</pre>

Safely remove your SD card and place it in your Raspberry Pi.  
No worry, you&#8217;ll be able to enjoy a trial period :-).

To continue, please refer to the original reference material: 

  * [HomeSeer HS3 quick-start guide][3]
  * [HS3-Pi release forum post][4] 
  * [HomeSeer HS3-Pi install guide][2] 

Also, read more @ [HS3-Pi hands-on part 2][5]

 [1]: ftp://ftp.homeseer.com/pub/HomeSeer-HS3Pi-Image.zip
 [2]: http://homeseer.com/guides/HomeSeer-HS3Pi-Guide.pdf
 [3]: http://www.homeseer.com/guides/HomeSeer-QuickStart-Guide.pdf
 [4]: http://board.homeseer.com/showthread.php?t=169252
 [5]: 2014/07/20/hs3-pi-hands-on-part-2
