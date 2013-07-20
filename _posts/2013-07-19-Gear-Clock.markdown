---
comments: true
date: 2013-07-19 14:30:00
layout: post
slug: Gear Clock
title: Gear Clock
summary: 'The Gear Clock'
image: 'Gear-Clock\front.thin.jpg'
tags:
- Projects
- Arduino
---


Awhile ago, I got man hands on an old and broken printer, not the desktop kind, but large small office kind. I took it apart for parts. I was intreguid by the gear mechanism for one of the paper feeders. I decided to make a clock out of it.

[![](/img/posts/Gear-Clock/front.web.jpg)](/img/posts/Gear-Clock/front.web.jpg)

There is a large gear that is marked out for the minutes and a smaller gear that is marked for the minutes. Because of the way the mechanism is built, the minute gear needs to spin counter clockwise. As the minute gear moves, it moves the gears and arms around it.

The clock is driven by an Arduino Uno with the Adafruit motor shield. Both the minute gear and the hour gear are driven by stepper motors that came out of the same printer. The steppers are much more powerful than they need to be, but I liked the idea of only using parts from the printer to build the clock.

[![](/img/posts/Gear-Clock/back.web.jpg)](/img/posts/Gear-Clock/back.web.jpg)