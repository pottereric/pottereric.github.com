---
comments: true
date: 2015-11-21 14:30:00
layout: post
slug: increment-and-decrement-deep-dive
title: Increment and Decrement Deep Dive
summary: 'A detailed look at the differences between the increment and decrement operators.'
image: 'the-joy-of-making-things\RainBarrel.jpg'
tags:
- C#
--

Recently a read a blog post by Eric Lippert about the top ten things he wished had been designed differently for C#. If you have not read it, [you can find it here.](http://www.informit.com/articles/article.aspx?p=2425867) It is worth reading in it's entirety. The section that got me thinking was "#3: I rate plus-plus a minus-minus". In it, he talks about his dislike of the increment and decrement operators. He makes very solid points. Firstly he points out that the increment operator can easily be replaced with "x += 1;". More importantly, he shows that the increment operator has two purposes, to return a value and alter the value of the variable. So by it's very definition, the expression has a side effect.

But the following statement is the one that grabbed my attention. 

> Next, almost no one can give you a precise and accurate description of the difference between prefix and postfix forms of the operators. The most common incorrect description I hear is this: "The prefix form does the increment, assigns to storage, and then produces the value; the postfix form produces the value and then does the increment and assignment later."

This explanation, that Lippert is saying is wrong, is the exact way that I was taught that it worked. Granted, I was taught originally in C++, and this may be true for how C++ works. I have always assumed that C# worked the same way. Lippert is saying that my assumption is wrong.

He goes on to describe what it really does.

> Why is this description wrong? Because it implies an order of events in time that is not at all what C# actually does. When the operand is a variable, this is the actual behavior:

> 1. Both operators determine the value of the variable.
2. Both operators determine what value will be assigned back to storage.
3. Both operators assign the new value to storage.
4. The postfix operator produces the original value, and the prefix operator produces the assigned value.

