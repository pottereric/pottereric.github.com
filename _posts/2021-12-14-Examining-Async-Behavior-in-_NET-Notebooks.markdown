---
comments: true
date: 2021-12-14 4:00:00
layout: post
slug: examining-async-behavior-in-_net-notebooks
title: "Examining Async Behavior in .NET Notebooks"
summary: "What can .NET Notebooks display when their code executes asynchronously?"
image: 'examining-async-behavior-in-_net-notebooks\lead.png' 
tags:
- C#
---

This post was written and published as part of the [2021 C# Advent](https://www.csadvent.christmas/).

One of my favorite new tools is the .NET Interactive Notebooks plugin for Visual Studio Code. It allows you to intermingle executable code and markdown descriptions of it. So you can explain the code, run the code, and see its results all in one place. This makes the notebooks incredibly useful for teaching and exploring concepts. 

One nice feature of Notebooks is that the display function returns an object that can update the displayed value. So unlike console functions that display a list of updated values, Notebooks allow you to update values in place. 

I wanted to know what Notebooks could do with asynchronous code. So I created two simple methods that code runs for a long enough period that their asynchronous behavior would be obviously noticeable. Both functions display their current activity and continuously update it in place. 

[![](/img/posts/examining-async-behavior-in-_net-notebooks/LongRunningFunctions.png)](/img/posts/examining-async-behavior-in-_net-notebooks/LongRunningFunctions.png)

Then I invoke both functions, assign their tasks into variables, and then use Task.AwaitAll to wait until both functions run to completion. When the code is executed, you can see that both functions are executing at the same time. (Yes, I know that they aren't necessarily running simultaneously at the CPU level.)


[![](/img/posts/examining-async-behavior-in-_net-notebooks/WhenAll.gif)](/img/posts/examining-async-behavior-in-_net-notebooks/WhenAll.gif)

Now that we understand the Notebook behavior a little better, we can run some experiments. What happens when we square all the values from 1 to 100 but only cube the values from 1 to 50? We see that the cube function finishes much earlier. What happens when we change the WhenAll function to WhenAny? We see that the squares function stops executing when the cube function completes. 

[![](/img/posts/examining-async-behavior-in-_net-notebooks/WhenAny.png)](/img/posts/examining-async-behavior-in-_net-notebooks/WhenAny.png)

The beautiful part of working with .NET notebooks is that you can experiment with the code right in the notebook. I encourage you to head over to the [GitHub repo](https://github.com/pottereric/DotNetInteractiveNotebooks) to download the notebook and try it yourself.
