---
comments: true
date: 2017-07-08 14:30:00
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

## Racing the Beam ##

I recently read 'Racing the Beam' and the most fascinating thing about it was that the code described in the book had to be intimately aware of the hardware in the Atari 2600**. It was a stark contrast to the code execution environments that web developers work in these days. 

The title of the book, Racing the Beam, acknowledges the fact that the Ataris were built to run with old CRT TVs that worked by continuously painting the screen with an electron beam. Because the Atari was single threaded and it did not have a graphics processor, the code for the actual game logic could only run while the beam was moving back to the left to get ready to paint the next line or back to the top to paint the next frame. The rest of the time the processor was responsible for painting the screen.

> "The programmer must carefully "cycle count" processor instructions so they execute at the right time."

The fact that the developers had to count CPU cycles is incredible. What is just as astonishing is that the machine only had **128 bytes of RAM**. Bytes. Not Gigabytes, or Megabytes, or Kilobytes. Bytes. As a point of comparison, my iPhone has 128 GB of storage.It literally has a billion times more capacity than the 2600. 

[![](/img/posts/Lessons-From-The-Atari-2600/AtariAndiPhone.jpg)](/img/posts/Lessons-From-The-Atari-2600/AtariAndiPhone.jpg)

When I was writing software for Palm OS, I had to support devices that only had 1 MB of RAM and that seems tiny. A web developer would do better being constrained to only using half a keyboard than trying to get anything done in 128 bytes. To be fair, the code was not loaded into memory but was instead executed directly from the cartridge ROM. But that is still a minuscule amount of memory. 

## Technical Wizardry ##

The cartridges didn't have much ROM space either. These limitations forced the programmers to be very creative. In the popular game Yars' Revenge, the developer wanted to place have a multicolored safe zone.  But creating a bitmap for this safe zone would take up too much memory. So he loaded chunks of the code itself as the bitmap. So when you are playing the game, you are seeing the game's code rendered as an image.

Yar's Revenge has another technique that really blew my mind. The developer knew the opcode for a function return statement and he had a sprite that happened to start with that same hexadecimal code. So he laid out the ROM so that the first byte of the sprite could also serve and the return statement of the previous method. 

> "In this code, then, the value $60 serves two purposes, as the opcode RTS when it is encountered in program flow and as the value $60 (binary %01100000) when it is read as data. As with the rendering of the Yars’ Revenge neutral zone, this is an example of the use of the contents of ROM—only a single byte, in this case—as both code and data."

One of the things that made this book great for me was that I remember playing these games. I remember them fondly as a form of entertainment. Now I also get to appreciate them as brilliant accomplishments in software development. 

The book spends a lot of time talking about the great lengths that the developers had to go through to render graphics on the screen. It doesn't spend as much time talking about the personalities involved, such as Nolan Bushnell. Those stories are covered in other books. This book stays very technical. It spends a lot of time talking about the capabilities and limitations of the hardware. I can't do the book justice to try to summarize it here. But I would strongly recommend that you go read it for yourself. 

[![](/img/posts/Lessons-From-The-Atari-2600/RacingTheBeam.jpg)](https://www.amazon.com/Racing-Beam-Computer-Platform-Studies/dp/026201257X)

## Lessons Learned ##

The primary lesson that I learned from this book was about the value that a developer can get from a deep knowledge of their platform. Even though the platforms that I develop for have far more resources, knowing exactly what can be done enables clever solutions. Having a deep knowledge of the platform enables me to use it to it's full potential. 

Just as the game developers for the Atari 2600 had a deep knowledge of the hardware they were running on and a very detailed knowledge of the TVs they were using as display, I should have a [deep knowledge](http://blog.apterainc.com/custom-software/should-custom-software-developers-be-generalists-or-a-specialists) of the web frameworks that I use and the web servers that run them. This kind of knowledge will help me build faster, better looking applications for my users.

---
Hat tip to Matt Groves. It was episode 16 of his Cross Cutting Concerns podcast that first introduced me to the book. Check out [the episode](http://crosscuttingconcerns.com/Podcast-016-Matt-Bok-on-Retro-Gaming-Tech) for yourself. 

---
* Yes, I know this isn't strictly true. But that is outside the scope of this post. 

** The console was originally released as the Atari VCS. The book sticks with that name. I remember it from my childhood as the Atari 2600 and I can't break the habit of using that name.
