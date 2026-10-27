---
title: From HomeSeer HS3 to Home Assistant
author: iHomeAutomate
excerpt: 'I never made the jump to the latest HomeSeer versions. HS3 was the last one I used, until I moved to Home Assistant in the last silent years ;-)'
permalink: /2026/10/27/from-homeseer-to-home-assistant/
categories:
  - homeseer
tags:
  - homeseer
  - hs3
  - home_assistant
  - z-wave
  - x10
  - energy
  - mqtt
  - rfxcom
  - irtrans
  - infrared
published: true
comments: false
---
This blog started as a place to share tips and experiences about HomeSeer, so it feels strange to write this one: I moved my home automation to Home Assistant in the last silent years ;-)

I never upgraded to the latest HomeSeer versions. HS3 was the last HomeSeer version I ran, and it stayed that way until the switch.

## Staying on HS3

HS3 did what I needed it to do, and every upgrade I skipped was one less thing to migrate. When a system works, "if it ain't broke, don't fix it" is a perfectly good strategy. Over time, though, the gap between my setup and where the rest of the home automation world was heading kept growing.

## Why Home Assistant

* **Open source and local-first**: it runs in your own home and does not depend on a cloud service.
* **A huge integration catalogue**: devices and services that were hard to connect to HS3 are often a few clicks away.
* **An active community**: new integrations, fixes and ideas show up constantly.
* **Modern Z-Wave and Zigbee support**: the technologies I already relied on are well supported.
* **Built-in Energy dashboard**: native support for tracking consumption, solar, and grid return out of the box.

## The Z-Wave network

The very first part of the system that made the leap was the Z-Wave network.

Z-Wave was always the backbone of my HomeSeer setup—controlling lights, switches, micro-modules, and sensors. Because so much of the house depended on it, a "big bang" switch wasn't an option. Breaking the house all at once while figuring out a new platform would have been painful.

Instead, I chose a gradual, side-by-side migration:

* **Two separate machines, two separate sticks:** I kept HomeSeer running on its own hardware with its original Z-Wave stick, while setting up Home Assistant on a dedicated machine with a second Z-Wave USB stick.
* **Two parallel networks:** This allowed both environments to run at the same time without interfering with each other.
* **Device by device:** I could exclude a single node from the HomeSeer network, immediately include it into Home Assistant, configure its entities, and test the automations—all while the rest of the house kept functioning uninterrupted on HS3.

Migrating device by device takes time, but running parallel networks gave me peace of mind. It meant I could take as long as I needed to learn Home Assistant's way of doing things without plunging the living room into darkness.

## Goodbye X10 and CM15A: no migration needed

Another legacy chapter that finally came to a close was X10.

Way back when this blog began, the CM15A USB transceiver was an essential bridge for X10 appliance and lamp modules. Over the years, however, powerline X10 had already been showing its age. Because I had previously replaced those old X10 modules with Z-Wave micro-modules, there was simply no need to bring X10 over to Home Assistant at all.

With the Z-Wave network already up and running in Home Assistant, those circuits were already taken care of. The CM15A and X10 hardware could simply be retired for good—one less legacy protocol to worry about.

## Energy metering: moving to P1

With the lights and essential Z-Wave devices safely transitioned, the next priority was house-wide energy monitoring: tracking electricity and gas consumption.

In HomeSeer, I had been monitoring energy using RFXCOM hardware. While that had served its purpose well during the HS3 era, transitioning to Home Assistant was the right moment to rethink the setup and move to something more modern and direct:

* **Switching from RFXCOM to P1 meters:** Instead of using RFXCOM receivers and transmitters, I plugged straight into the smart meter's P1 port. 
* **Direct digital data:** The P1 meter reads the telegrams directly from the utility meter, delivering accurate, real-time electricity (consumption and return) and gas readings without intermediate wireless conversions.
* **Plugging into Home Assistant's Energy dashboard:** Home Assistant's built-in Energy management was a massive upgrade. Feeding the P1 meter entities directly into the Energy dashboard gave me instant hourly, daily, and monthly breakdowns with virtually zero configuration overhead.

Getting accurate energy and gas data into Home Assistant right after Z-Wave meant the new setup was already providing real daily value.

## Retiring RFXCOM: 433 MHz sensors over MQTT

While the energy metering moved directly to the P1 port, I still had a variety of 433 MHz sensors across the house that originally reported into HomeSeer through RFXCOM.

Rather than keeping the RFXCOM hardware around or trying to link it into Home Assistant, I decided to decommission it entirely:

* **A custom-built application:** I built a custom application to handle and parse the incoming 433 MHz sensor signals.
* **Publishing to MQTT:** The application decodes the sensor payloads and publishes the data cleanly over MQTT.
* **Native Home Assistant integration:** Through Home Assistant's MQTT integration (and MQTT discovery), each 433 MHz sensor automatically surfaces as a clean, native entity—temperature, humidity, motion, and more.

This allowed me to fully retire the old RFXCOM setup without having to replace dozens of perfectly working 433 MHz sensors.

## The final piece: Infrared with IRTrans

The very last integration to make the jump was infrared control.

Back in the early days of this blog, IRTrans was a core component for controlling AV equipment, TVs, and entertainment gear from HomeSeer. Despite all the newer IP-controllable and smart devices on the market, reliable, local IR hardware remains difficult to replace when you have classic or standalone equipment.

The great news: the IRTrans hardware is still running strong. Instead of retiring it, I brought it straight into Home Assistant. With IRTrans connected to the network and integrated into Home Assistant, I can still trigger all the necessary IR commands and automations locally.

Bringing IRTrans across the finish line meant the migration was officially complete: every core capability of my old HS3 installation had found a modern, stable home in Home Assistant.

## What I miss from HS3

Honestly? Nothing.

One of the persistent pain points in the HomeSeer ecosystem was plugin compatibility. Every time a new core version dropped, there was always that hesitation: would third-party or paid plugins break? From time to time, plugins simply weren't ready or compatible yet with the latest releases, leaving you stuck on older versions just to keep your setup working.

Home Assistant has been a breath of fresh air in comparison:

* **Completely free:** No licensing costs for core software or paid plugins for standard integrations.
* **Rock-solid release cycle:** Updates roll out monthly like clockwork, packed with improvements, performance tweaks, and new device integrations.
* **Zero compatibility headaches:** Across all the updates, I have never run into broken integrations or incompatibilities. It just updates, restarts, and runs.

## What happens to this blog

The HomeSeer articles stay online. Plugins, scripts and changelogs from the HS3 era may still help someone who runs it today.

Since completing the transition, my setup on Home Assistant has expanded tremendously—far beyond what I ever had running under HS3. Expect plenty more posts about Home Assistant, custom setups, and new projects on this blog in the future!
