---
comments: true
date: 2015-01-19 14:30:00
layout: post
slug: ScriptCS-Arduino controlled Nerf gun
title: ScriptCS-Arduino controlled Nerf gun
summary: 'ScriptCS-Arduino controlled Nerf gun'
image: 'ScriptCS-Arduino-controlled-nerf-gun\Preview.JPG'
tags:
- Arduino
---

[![](/img/posts/ScriptCS-Arduino-controlled-nerf-gun/Full.JPG)](/img/posts/ScriptCS-Arduino-controlled-nerf-gun/Full.JPG)

One night I was hanging out with my sons. We were talking about robotics and one of them asked if I could build a robot that would fire a Nerf gun. So we started out with a bunch of parts I had on hand to see if we could do it. I mounted the Nerf gun to a piece of peg board and then set out to see what I had that could pull the trigger. My first attempt was to use a motor that was geared way down to pull back a string that was attached to the trigger. I used an Arduino with a motor sheild to control the motor. That worked but it was slow. Since the boys were bored with a Nerf gun that took 5 seconds to fire, we called it a night.

To make it faster, I ordered a 24V Solenoid from Adafruit. I had a AC adapter that I salvaged out of an old printer that I used to power the solenoid. To control the higher voltage, I used a TIP120 transistor I got from RadioShack. Now I could fire the Nerf gun almost instantly with the press of a button.

To make it more interactive, I started controlling the Arduino with the [ScriptCS-Arduino](http://www.humbletoolsmith.com/2014/04/04/Getting-Started-With-ScriptCS-Arduino/) library. This made it controllable from my laptop.

A few weeks later, I came across an old 5 disk CD changer. I took out most of the electronics and soldered longer wires onto the motor that spins the tray. I wired the motor up to the 24V source I was using for the solenoid and controlled that with another TIP120.

[![](/img/posts/ScriptCS-Arduino-controlled-nerf-gun/Circuit.png)](/img/posts/ScriptCS-Arduino-controlled-nerf-gun/Circuit.png)

In the original version, the wires went straight from the Arduino up to the solenoid. The was functional, but it meant that if I spun it around too much, the wires would get twisted or unplugged. This got old after a few weeks.

I decided that I wanted the gun to spin freely, but I needed away to get the control voltage up to the solenoid. Inspired by Ben Heck's [Steampunk Persistence of Vision Display](https://www.youtube.com/watch?v=1reDoTu6L5w "Steampunk Persistence of Vision Display"), I mounted two metal rings on the bottom of the CD tray.

[![](/img/posts/ScriptCS-Arduino-controlled-nerf-gun/rings.JPG)](/img/posts/ScriptCS-Arduino-controlled-nerf-gun/rings.JPG)

On the base, I mounted to spring mounted contacts that would create a connection to the rings above. The allows the circuit to be complete no matter what position the CD tray was in. If I had a 3D printer like Ben Heck, the build would have been much cleaner.

[![](/img/posts/ScriptCS-Arduino-controlled-nerf-gun/contacts.JPG)](/img/posts/ScriptCS-Arduino-controlled-nerf-gun/contacts.JPG)

Over time, I continued to make improvements. I got a prototyping shield for the circuit. I got some standoffs and mounted the whole thing under the CD tray.

[![](/img/posts/ScriptCS-Arduino-controlled-nerf-gun/Arduino.JPG)](/img/posts/ScriptCS-Arduino-controlled-nerf-gun/Arduino.JPG)

One problem that I had was that the motor drove the CD tray with a rubber band. If I put the full 24V on the motor immediately, the band would often slip. So what I decided to do was use the PWM functionality of ScriptCS-Arduino to spin the motor slowly at first and then accelerate. The made the motor spin much more reliably. 

<script src="https://gist.github.com/pottereric/a95a3f9925e28bab72fb.js"></script>

The full source code is available on GitHub in a file named [NerfGunExample.csx](https://github.com/pottereric/scriptcs-arduino_examples/blob/master/NerfGunExample.csx)

It is far from perfect. I am putting a lot more weight on the CD than it was designed for, so it will certainly break at some point. The control for the motor is very crude. At the very least, I should use an H-bridge so that I could spin the gun in both directions. It would be even better if I used a stepper motor so that I had much more precise control over the movements. 

But it is fun to play with. It demonstrates many of the things about ScriptCS-Arduino that I really like. It is fun to play around with. Here it is in action.


<iframe src="//player.vimeo.com/video/116514637" width="500" height="331" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe> <p><a href="http://vimeo.com/116514637">ScriptCs-Arduino Controlled Nerf Gun</a> from <a href="http://vimeo.com/user7221255">Eric Potter</a> on <a href="https://vimeo.com">Vimeo</a>.</p>
