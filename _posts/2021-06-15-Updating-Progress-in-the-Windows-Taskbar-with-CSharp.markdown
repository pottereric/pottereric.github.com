---
comments: true
date: 2021-06-15 4:00:00
layout: post
slug: updating-progress-in-the-windows-taskbar-with-csharp
title: "Updating Progress in the Windows Taskbar with C#"
summary: "Building a simple Pomodoro Timer that displays progress in the Taskbar"
image: 'updating-progress-in-the-windows-taskbar-with-csharp\lead.png' 
tags:
- C#
---

I've been using the Pomodoro Technique to structure my work day for a few years I find it very helpful to plan and focus my work. But it requires a timer. I have used [Tomighty](https://tomighty.github.io/) and [PomoFocus.io](https://pomofocus.io/), but I wanted something different.

I wanted a way to see the status of the pomodoro at a glance. I decided to try to use the Windows API that allows apps to display their progress in the taskbar to display the progress of a 25 minute pomodoro session. 

[![](/img/posts/updating-progress-in-the-windows-taskbar-with-csharp/Pomodoro in the taskbar.png)](/img/posts/updating-progress-in-the-windows-taskbar-with-csharp/Pomodoro in the taskbar.png)

I wasn't sure how to update the progress from a Windows Forms app, but then I came across the [Microsoft-WindowsAPICodePack Nuget package](https://www.nuget.org/packages/Microsoft-WindowsAPICodePack-Core/). It provides two simple methods to manipulate the progress with the taskbar icon. 

The first is the SetProgressState, which takes a enum which can be NoProgress, Indeterminate, Normal, Error, or Paused. The normal state puts a green overlay on the icon. I use the Normal state for the first 20 minutes of a pomodro. The Paused state makes the icon yellow, which I use to indicate that the pomodoro has less than 5 minutes remaining. The Error state makes the icon red, which I use to indicate the pomodoro is over.

The second method is SetProgressValue. This takes a current value and a max value and renders the progress bar as an overlay on the icon. I pass the current minute of the pomodoro as the current value and 25 as the max value. 

So far, I've been pleased with the results. The information is "glancable" without taking up additional real estate on my screen. 

If you want to see the code, I've posted [the repo on GitHub.](https://github.com/pottereric/PomodoroProgressBar)
