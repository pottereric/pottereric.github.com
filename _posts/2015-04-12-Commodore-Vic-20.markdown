---
comments: true
date: 2015-04-12 14:30:00
layout: post
slug: Commodore Vic 20
title: Commodore Vic 20
summary: 'Impressions of a 30 year old PC'
image: 'Commodore-Vic-20\FrontPageImg.jpg'
tags:
- fun
- make
- retro
---

I stopped by the Salvation Army last weekend to make a donation. When I went into get a receipt, I noticed that they had a Commodore Vic-20 on the shelf. I've heard about this machine many times on the Hello World podcast and was instantly fascinated by it. When I realized it still had the original manuals with it, I bought it.

[![](/img/posts/Commodore-Vic-20/Box.jpg)](/img/posts/Commodore-Vic-20/Box.jpg)

Some of the things that are advertised on the packaging are quire humorous. It has a "typewriter-style keyboard." When was the last time that was listed as a feature of computer. It was "the friendly computer." Which is true if you consider booting straight into a BASIC interpreter to be friendly. I would still consider this a feature (albeit with a different language), but I assume I am in the minority here. It came with "arcade game excitement." Technically this was true. More on that later.

[![](/img/posts/Commodore-Vic-20/CommodoreVic20.jpg)](/img/posts/Commodore-Vic-20/CommodoreVic20.jpg)

It has the classic Commodore construction where the entire computer is housed under the keyboard. It was also manufactured before keyboard layouts were standardized. All of the letters are where you would expect them to be, but after that there are major differences. As a C# and JavaScript developer, I noticed right away that the semicolon isn't were modern keyboards have it. Maybe most notably, it has a key for pound (£), which modern keyboards don't have. In fact, I had to insert a 'special character' to include the symbol in the previous sentence. Noticeably absent are the arrow keys and the escape key. The biggest disappointment was that the keyboard use rubber membrane switches and not something with a spring in it like the Apple II had or the IBM model M keyboards had.

[![](/img/posts/Commodore-Vic-20/Books.jpg)](/img/posts/Commodore-Vic-20/Books.jpg)

One of my favorite things about this purchase is that it came with the original literature. Look how much fun that family is having working on the spreadsheet for their family budget.

[![](/img/posts/Commodore-Vic-20/Manual.jpg)](/img/posts/Commodore-Vic-20/Manual.jpg)

It only takes seven pages before the owners manual is telling you how to write your first program. The rest of the 164 page owners manual is a introduction to programming. 

[![](/img/posts/Commodore-Vic-20/Code.jpg)](/img/posts/Commodore-Vic-20/Code.jpg)

Now when box said it came with "arcade style fun", what it meant was that it came with a book of source code for a bunch of different games. So what you had to do was boot up the computer, type in a few hundred lines of code perfectly, then you could play the game. To be fair, there were cartridges you could buy or a cassette tape drive you could use to load games, but those were extra. My purchase didn't come with either. 

I was able to hook it up to my TV and it turned on right away. But I immediately noticed that about half of the characters did not display correctly. 

[![](/img/posts/Commodore-Vic-20/Screenshot.jpg)](/img/posts/Commodore-Vic-20/Screenshot.jpg)

As I typed, some of the characters displayed properly and some displayed as solid blue boxes. Interestingly, when you line the characters up in ASCII order, 4 in a row will display properly and the next four will fail. This pattern holds for all characters. In fact an character whose ASCII has the 3rd bit (the one whose decimal value is 4) set to 1 would not display properly. If I typed in the code, it would execute perfectly, other than the display. So the problem is somewhere in the display circuitry. 

[![](/img/posts/Commodore-Vic-20/Motherboard.jpg)](/img/posts/Commodore-Vic-20/Motherboard.jpg)

I opened up the device to see if there was anything obviously wrong. I didn't see anything that looked to be causing the malfunction, but it was interesting to see how it was built. This was before everything was built with surface mount electronics. 

[![](/img/posts/Commodore-Vic-20/Chips.jpg)](/img/posts/Commodore-Vic-20/Chips.jpg)

All of the components are full sized, through-hole soldered components. The chips aren't all combined into integrated circuits. In fact many standard TTL chips are on the board. There is a very standard looking 555 chip near one of the expansion ports. 

Because it doesn't work properly and because any software I could run on this I could easily run in an emulator, I'm going to dissemble this one and turn it into something else. More on that in a future post. 
