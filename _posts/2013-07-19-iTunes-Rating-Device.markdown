---
comments: true
date: 2013-07-19 14:30:00
layout: post
slug: The iTunes Rating Device
title: The iTunes Rating Device
summary: 'The iTunes Rating Device'
image: 'iTunes-Rating-Device\front.thin.jpg'
tags:
- Projects
- Arduino
---



I built this box so that I could easily change the rating of songs in iTunes. The idea is that if iTunes is playing while the window is mimimized or hidden, I want to know the current rating and change it without switching to the iTunes window.

[![](/img/posts/iTunes-Rating-Device/front.web.jpg)](/img/posts/iTunes-Rating-Device/front.web.jpg)

The box has 5 LEDs that display the number of stars currently assigned to the track. Then there is a nob that increases the star rating when it is turned to the right and decreases the start rating when turned to the left. Lastly, there is a red play/pause button. 

There is software that runs on the computer that recieves these inputs. It forwards the commands on to iTunes via it's COM interface.

The box is built around a phidgets board. (http://www.phidgets.com/). Phidgets are unique in that all of the processing is done on the computer and the board is simply an IO device. The board is conected to the computer by USB. The program is written in C# using the Phidgets libraries. 

The Phidgets hardware was very easy to use. It does have the limitation of needing to be teathered to a PC. But for this project, that was perfect.