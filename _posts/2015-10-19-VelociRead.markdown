---
comments: true
date: 2015-10-19 14:30:00
layout: post
slug: VelociRead
title: VelociRead
summary: A project to for controlled speed reading.
image: 'VelociRead\HomePage.JPG'
tags:
- Arduino
- C#
---

So I had this idea. I had been using speed reading sites like [Spreeder](http://www.spreeder.com/) and [Spritz](http://spritzinc.com/). They accelerate your speeding by only showing you one word at a time. The words are always in the same place, so you don't have to move your eyes. I found them to be a very helpful way to get through my daily reading list. The only problem was that at times I wanted to vary the speed at which I was reading. Both of those tools move from one word to the next at a fixed rate.

I often try to read while on my stationary bike. I thought it would be interesting to try to control how fast speed reader moved using the bike. This would allow me to get through less interesting parts of the reading by pedaling faster. Conversely, I could pedal slower if I wanted to read part of it more carefully.

I realized that the device on my stationary bike that showed my "speed" was connected to the bike by a wire with two pins. 

[![](/img/posts/VelociRead/Plug.JPG)](/img/posts/VelociRead/Plug.JPG)

In order to figure out what they do, I hooked by bike up to an oscilloscope. I don't have a real oscilloscope, so I decided to try out some software I had read about on the [Make blog](http://makezine.com/projects/sound-card-oscilloscope) called '[Soundcard Oscilloscope](https://www.zeitnitz.eu/scope_en)'. It isn't as nice as a real scope, but it did everything that I needed it to do.

Using the software, I was able to tell that it omitted a high pulse once per revolution of the pedals. So I figured if I could convert that pulse into something meaningful to my PC, I would be able to make the project work.

Since I only had one input, I decided to use a [Digispark](http://digistump.com/products/1) microcontroller. The Digispark also has a library that allows it to function as a USB keyboard. I programmed the Digispark to act as if a 'j' had been typed on the keyboard once per pedal revolution. I found a connector that matched the connector for the stationary bike. I soldered the connector to the Digispark, leaving a few feet of wire between them.

I created my own clone of Spreeder using WPF. Instead of advancing from one word to the next at a fixed interval, it advances at a rate that is proportional to how fast I am pedaling. I added keyboard shortcuts to move to the next or previous chapter. I also added shortcuts to move forward or back 50 words. If you care to see it, the source code is [here](https://github.com/pottereric/VelociRead).

Because of the additional keyboard shortcuts, I wanted to be able to have a keyboard near the bike. I removed the PCB from a cheap USB hub. I plugged the DigiSpark and another USB keyboard into the hub. I put the combination into an Altoids tin. 

[![](/img/posts/VelociRead/Adapter.JPG)](/img/posts/VelociRead/Adapter.JPG)

The results have been satisfactory. I have read several books this way. I am continuing to make some tweaks to the software to improve the reading experience. But overall the project was a success.

