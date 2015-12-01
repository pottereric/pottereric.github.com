---
comments: true
date: 2015-12-01 14:30:00
layout: post
slug: Go-To-Implementation
title: Go To Implementation
summary: 'There is a great new feature in VS2015 Update 1.'
image: 'Go-To-Implementation\link.png'
tags:
- C#
- Visual Studio
---


Yesterday Microsoft released Update 1 for Visual Studio 2015. There are a host of great features that were added. There are other blog posts that cover all of the features that are included. I just want to highlight the one that I am most excited about. 

In the previous versions of Visual Studio, you had the ability to right click on a method invocation statement and click 'Go To Definition'. This would take you to the code that defines that method. This is a great feature, but with our modern development practices, it left something to be desired.

More and more, we are developing code that makes use of interfaces. This is for a lot of good reasons. They make the code more testable and they help developers encapsulate functionality. But if you were in Visual Studio and you clicked 'Go To Definition' on an object that was defined as an instance of an interface, you would be taken to the definition in the interface, not to the code that defines the method.

There is where the beauty of the 'Go To Implementation' feature comes in. Now if you click on the same method invocation, you get an additional option to go to the implementations of the method.

[![](/img/posts/Go-To-Implementation/MenuOption.png)](/img/posts/Go-To-Implementation/MenuOption.png)

If there is only one implementation, you will be taken directly to it. If there are multiple implementations, you will be given a list that you can choose from.

This isn't a huge feature, but it is one that I will use almost daily. While Resharper has had this feature for awhile, I am really glad that this is now directly in Visual Studio.