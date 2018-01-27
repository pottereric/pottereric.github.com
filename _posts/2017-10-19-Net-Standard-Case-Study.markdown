---
comments: true
date: 2017-10-19 14:30:00
layout: post
slug: net-standard-case-study
title: Net Standard Case Study
summary: 'A practicle look at the growth of .Net Standard'
image: 'Net-Standard-Case-Study\layers.png'
tags:
- NetStandard
---

Much has been written about how many APIs have been added to .Net Standard between version 1.1 and 2.0. I wanted to share a practical example of how this API growth has improved the product. 

There is an NES emulator named [Nintaco](http://nintaco.com/). It can be controlled via an [API](http://nintaco.com/api.html), meaning that you can write a bot to play an NES game. There are API examples in several languages including C#. I got permission from the author to bundle the C# API as a NuGet package. I wanted to make the package a .Net Standard class library so that could have the widest possible audience. But when I first tried to create the NuGet package, it couldn't compile under .Net Standard, which at the time was a version 1.1. 

To integrate with the Nintaco API, the emulator makes some sockets available and the API talks to them over TCPIP. Many of the networking APIs where missing from .Net Standard as of version 1.1. Here were the errors that I got:

* The type or namespace name 'Sockets' does not exist in the namespace 'System.Net' 
* 'BinaryWriter' does not contain a definition for 'Close' 
* 'BinaryReader' does not contain a definition for 'Close'
* The type or namespace name 'TcpClient' could not be found 
* The type or namespace name 'BufferedStream' could not be found 
* The name 'Thread' does not exist in the current context	

It makes sense that the networking and threading APIs would be missing initially because they are obviously coupled to the underlying operating system, making them more complex to write in a cross-platform environment. But this prevented me from being able created .Net Standard 1.1 library for the Nintaco API.

In .Net Standard 1.3, the Sockets class was added, resolving one of the errors. 

In .Net Standard 1.5, the BufferedStream class was added, resolving another of the errors. This left 4 errors. 

In .Net Standard 2.0, all of the remaining classes that I needed were added. So while the missing classes were a deal-breaker in .Net Standard 1.1, version 2.0 had absolutely everything I needed. The package is now published to the [NuGet]( https://www.nuget.org/packages/NintacoProxy/) repository. I'll have more about how to use the package in a future blog post. 

