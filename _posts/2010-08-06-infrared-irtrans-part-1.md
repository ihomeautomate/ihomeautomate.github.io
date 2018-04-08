---
title: IR home automatisation using irTrans (part 1)
author: iHomeAutomate
excerpt: 'A first experience doing infrared home automatisation with irTrans'
layout: article
permalink: /2010/08/06/infrared-irtrans-part-1/
image:
  teaser: logo_irtrans-400x250.jpg
categories:
  - infrared
tags:
  - infrared
  - ir
  - irtrans
ads: true
comments: false
---
Requisites:

<table width="100%">
  <tr>
    <td>
      <ul>
        <li>
          IRTrans Ethernet IRDB
        </li>
        <li>
          IRTrans Power Supply (not included by default)
        </li>
        <li>
          IRTrans 6 Way Transmitter
        </li>
        <li>
          IRTrans External Learning receiver (optional)
        </li>
        <li>
          IRTrans External Standard receiver (optional)
        </li>
      </ul>
    </td>
    
    <td align="right">
      <img src="http://www.irtrans.com/images.site/logo_irtrans.gif" alt="" />
    </td>
  </tr>
</table>

With the IRTrans device I can both send and receive IR codes, even over TCP/IP. The IRDB gives me the option to extend my IR device pool with future exotic IR codes that might appear. This way it&#8217;ll be possible to relay them easily. Using the IRDB it&#8217;s also possible to connect directly to the IRTrans device (via HTTP or TCP) and send a IR code from the DB.

The &#8220;6 Way Transmitter&#8221; allows me to transmit to 6 different devices. On the IR-received of each device we put a sender using a sticker. This enables us to reliably send signals over. The other side of the cable is connected to the IRTrans device.

The optional IRTrans External Standard receiver can be used to relay signals from outside a (closed) cabinet to the IRTrans module inside. Be aware, this receiver can only learn IR codes within the 36-40kHz range.

The IRTrans External Learning receiver, also optional, is similar to the Standard Receiver. However it does give you the ability to learn IR codes outside the standard frequency range. Be careful, the cable is only ~0,25m long!
