---
comments: true
date: 2015-01-04 14:30:00
layout: post
slug: C# and Microcontrollers
title: C# and Microcontrollers
summary: 'C# and Microcontrollers'
image: 'CSharp-and-Microcontrollers\CSharpAndMicroocontrollers.jpg'
tags:
- Arduino
---

There are plethora of microcontrollers available today. If you want to write your microcontroller code in C#, you have a couple of options. 

First lets look at how a standard Arduino works today. Standard Arduinos like the Arduino UNO are programmed from a computer. Once the code is loaded, they are fully autonomous from the computer. The Arduino has it's own processor and storage, so it doesn't need the computer to run.

[![](/img/posts/CSharp-and-Microcontrollers/Standard.jpg)](/img/posts/CSharp-and-Microcontrollers/Standard.jpg)

There is an open source IDE for Arduino that runs on your laptop. The code that write is in C. (Technically it is Processing, but it is very close to C.) 

[![](/img/posts/CSharp-and-Microcontrollers/Standard C.jpg)](/img/posts/CSharp-and-Microcontrollers/Standard C.jpg)


There is another board that you can purchase called the Netduino. It is more powerful and more expensive than an Arduino. 

[![](/img/posts/CSharp-and-Microcontrollers/PCNetduino.jpg)](/img/posts/CSharp-and-Microcontrollers/PCNetduino.jpg)


The code you write for the Netduino is C# and you use Visual Studio as the IDE. The Netduino has a processor that is powerful enough to run the .Net Micro Framework. So the code you write executes write on the Netduino. 

[![](/img/posts/CSharp-and-Microcontrollers/PCNetduino CSharp.jpg)](/img/posts/CSharp-and-Microcontrollers/PCNetduino CSharp.jpg)


5

[![](/img/posts/CSharp-and-Microcontrollers/ScriptCS.jpg)](/img/posts/CSharp-and-Microcontrollers/ScriptCS.jpg)


6

[![](/img/posts/CSharp-and-Microcontrollers/ScriptCS Firmata.jpg)](/img/posts/CSharp-and-Microcontrollers/ScriptCS Firmata.jpg)


7