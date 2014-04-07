---
comments: true
date: 2014-04-04 14:30:00
layout: post
slug: Getting-Started-With-ScriptCS-Arduino
title: Getting started with ScriptCS-Arduino
summary: 'Getting started with ScriptCS-Arduino'
image: 'Getting-Started-With-ScriptCS-Arduino\Arduino.jpg'
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

## Installing the Software

In this post, I'm going to show you how to get started with ScriptCS-Arduino, specifically on Windows PC. The first thing you need to do in order to use ScriptCS-Arduino is to install ScriptCS. The full details are available at [http://scriptcs.net/](http://scriptcs.net/). But if you have [Chocolatey](http://chocolatey.org/) installed, you only need to use the following command. (If you don't have Chocolatey installed, you should check it out. It is very useful.)

    cinst scriptcs

Next you will need to have the Arduino IDE installed. You can install it with this Chocolatey command.

    cinst arduinoide -Version 1.0.5.20130613

Or you can get it from the [Arduino software page](http://www.arduino.cc/en/Main/Software). With your Arduino connected to the PC, you need to load the Firmata library on to the Arduino. You don't need to download it because Firmata comes with the Arduino IDE. In the Arduino IDE, select "Standard Firmata" from the examples menu.

<iframe src="https://onedrive.live.com/embed?cid=78462497028D9B1F&resid=78462497028D9B1F%21440&authkey=ADWGgTOciE6ZekY" width="264" height="320" frameborder="0" scrolling="no"></iframe>

Load this software onto your Arduino. Make sure you have the right board and Serial Port selected in the Tools menu. Then click the Upload button.

Next you need to setup ScriptCS. One of the most powerful things about ScriptCS is that it is fully integrated with NuGet. The means that you can easily install ScriptCS-Arduino NuGet Package. ScriptCS-Arduino is a NuGet package specially designed for ScriptCS called a ScriptPack In your command shell of choice navigate to a directory where you want to work. Type the following command. 

    scriptcs -install scriptcs.arduino

This will install the NuGet package in your current directory. ScriptCS executes .csx files. Your .csx files in this directory can use the NuGet package you just downloaded. Here is a simple example of .csx file using ScriptCS-Arduino. It simply blinks and LED, which is basically the hello world of Arduino programming.

# Writing the Code

<script src="https://gist.github.com/pottereric/9978841.js"></script>

This script assumes that there is an LED with it's anode (positive side) connected to pin 9 on the Arduino and it's cathode (negative side) connected to ground.

Line 1 of the code imports the ScriptCS-Arduino ScriptPack. Line 2 creates an object that represents the Arduino board. Line 4 creates an instance of the Led class. The Led class is part of the ScriptCS-Arduino ScriptPack. It simplifies the code necessary to control an Led. Lines 6 through 9 dictate that the LED blink for 2 seconds and then stop. Line 11 cleans up all of the resources.

# Possibilities

This example is trivial and it could have been done entirely in the Arduino IDE. But ScriptCS-
Arduino opens up a host of great possibilities. The biggest opportunity is that you could integrate your Arduino into projects on your PC. For example, instead of just randomly blinking and LED for 2 seconds, you could run the script as a part of your build process and blink a red LED if there is a build failure and green LED if it succeeded. Because of the power of Arduino, you are not limited to LEDs. You could sound and alarm, spin something, or even fire a Nerf gun. The possibilities are nearly endless.

Another fantastic thing about ScriptCS-Arduino is that it allows you to prototype things very quickly. You can write little a script to try out just about any behavior of the Arduino. For those of us who know C#, it makes it faster to be working in a familiar language. You can use the ScriptCS REPL to make your Arduino exploration even more flexible. I'll explore this topic more in a future blog post.

# Get Started

You now know enough to get started. Use your imagination. Building something cool. Have some fun!

