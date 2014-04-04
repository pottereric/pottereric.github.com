---
comments: true
date: 2014-04-04 14:30:00
layout: post
slug: Getting-Started-With-ScriptCS-Arduino
title: Getting started with ScriptCS-Arduino
summary: 'Getting started with ScriptCS-Arduino'
image: 'the-joy-of-making-things\RainBarrel.jpg'
tags:
- ScriptCS
- Arduino
---

## Arduinos and PCs

I love making things with Arduino boards. The documentation is great. There are plenty wonderful accessories. And best of all, the community is amazing. For projects that are designed to be autonomous, it is hard to beat the Arduino.

But many of my projects are designed be used while connected to my computer. The Arduino supports serial communication which enables the Arduino and the PC to communicate. Some of the newer boards are powerful enough to emulate USB keyboards. The Arduino can simulate key presses, and the PC receives them as if a USB keyboard was sending the commands. This is how DigBug and VelociRead work. This is easy to develop, the but communication only flows from the Arduino to the PC. The Arduino can also open a serial connection which enables bidirectional communication. The drawback to this is that it takes more work to develop.

## ScriptCS-Arduino

Enter [ScriptCS-Arduino](https://github.com/luisrudge/scriptcs-arduino ). This fantastic library allows you to rapidly develop code in C# that controls the Arduino.  It was developed by Luis Rudge and is fully open source. It makes use of [ScriptCS](http://scriptcs.net/) to execute code on the PC and it uses the [Firmata](http://firmata.org/wiki/Main_Page) library to control the Arduino.

The execution model with ScriptCS-Arduino is different from standard Arduino programming. Normally, you would write all of your Arduino code in the Arduino IDE and write it to the Arduino board. With ScriptCS-Arduino, you use the Arduino IDE to load the Firmata code onto the Arduino and you do the rest with ScriptCS. Essentially, the Arduino board becomes a slave board. All of the important code runs on the PC.

## Getting Started 

In this post, I'm gonig to show you how to get started with ScriptCS-Arduino, specifically on Windows PC. The first thing you need to do in order to use ScriptCS-Arduino is to install ScriptCS. The full details are available at [http://scriptcs.net/](http://scriptcs.net/). But if you have [Chocolatey](http://chocolatey.org/) installed, you only need to use the following command. (If you don't have Chocolatey installed, you should check it out. It is very useful.)

    cinst scriptcs

Next you will need to have the Arduino IDE installed. You can install it with this Chocolatey command.

    cinst arduinoide -Version 1.0.5.20130613

Or you can get it from the [Arduino software page](http://www.arduino.cc/en/Main/Software). With your Arduino connected to the PC, you need to load the Firmata library on to the Arduino. You don't need to download it because Firmata comes with the Arduino IDE. In the Arduino IDE, select "Standard Firmata" from the examples menu.

<iframe src="https://onedrive.live.com/embed?cid=78462497028D9B1F&resid=78462497028D9B1F%21440&authkey=ADWGgTOciE6ZekY" width="264" height="320" frameborder="0" scrolling="no"></iframe>

Load this software onto your Arduino. Make sure you have the right board and Serial Port selected in the Tools menu. Then click the Upload button.

Next you need to setup ScriptCS. One of the most powerful things about ScriptCS is that it is fully integrated with NuGet. The means that you can easily install ScriptCS-Arduino Nuget Package. In your cammnd shell of choice naviagate to a directory where you want to work. Type the following command. 

    scriptcs -install scriptcs.arduino

This will install the NuGet package in your current directory. 


TODO

<script src="https://gist.github.com/pottereric/9978841.js"></script>

TODO

