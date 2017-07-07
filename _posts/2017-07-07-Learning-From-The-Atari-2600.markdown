---
comments: true
date: 2017-07-06 14:30:00
layout: post
slug: learning-from-the-atari-2600
title: Learning From the Atari 2600
summary: 'There is something fun about creating an object'
image: 'Lessons-From-The-Atari-2600\lead.jpg'
tags:
- fun
- retro
---

[![](/img/posts/Lessons-From-The-Atari-2600/Atart2600.jpg)](/img/posts/Lessons-From-The-Atari-2600/Atart2600.jpg)
The majority of the code I write completely abstracted away from the hardware it eventually runs on. If I am writing a Web API in C#, my code only knows what is will be run by the CLR, which may be running a server or an Azure host, but the code doesn't need to know which one. And it certainly doesn't need to know what kind of RAM is installed on the machine that it eventually runs on. It doesn't necessarily need to be concerned with how much RAM the machine has because it can safely* assume that there will be enough. And when I write client side code, it is even further removed from the hardware. 
