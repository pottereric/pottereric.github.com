---
comments: true
date: 2017-03-16 14:30:00
layout: post
slug: Pattern Matching on Types
title: Pattern Matching on Types
summary: 'Pattern Matching on Types'
image: 'Benefits-of-Pattern-Matching\MainPage.jpg'
tags:
- PatternMatching
- C#
---

In the [previous post](http://humbletoolsmith.com/2017/03/15/Pattern-Matching-and-Tuples/), there was a subtle feature that I didn't highlight. That was the fact that the switch statement was switching on a tuple, which is a struct. This might not seem like a big deal, but before C# 7.0, if you tried to switch on a struct, you would have gotten the following error message:

> "A switch expression or case label must be a bool, char, string, integral, enum, or corresponding nullable type."

What C# 7.0 gives us is the ability to switch on **any type** and match them with **Type Patterns**. It makes sense to match on classes when you consider that C# is an object oriented language. Where functional languages provide extra tools to match on lists (which are integral to functional programming patterns), C# gives us the ability to match on an object's place in the inheritance hierarchy.

You could make an argument that the client code shouldn't switch on the different types and that the different behaviors should be accessed through polymorphism. I would generally agree with that. But in many cases, you can't alter the classes you are working with. For example, if you are working with UI objects in a WPF application, you can modify the classes. 

So let's look at a WPF example. Let's say that you have a dialog that has multiple types of controls, and you need to be able to reset all of the controls back to their base state. The trick to this is that depending on the control, the reset behavior is different. We could do this in C# 6 with *if* statements, *is* checks and *as* casts. 

<script src="https://gist.github.com/pottereric/d5395a3ad03f359d109a45b971220152.js"></script>

Now let's look at the same code with C# 7.0 Pattern Matching.

<script src="https://gist.github.com/pottereric/bca51fb00ce548f9d90a7dd2a426eea6.js"></script>

First off, this cuts the number of characters inside the *foreach* loop from 252 down to 172 and it cuts down the number of lines by 3. What is more important is that the code is much more readable. 

Part of what makes this so much better is that the Pattern can declare a variable. So on line 10, if the control that is being matched is a ComboBox, a variable named cb will be created that is already a ComboBox. This removes the need for the *is* and the *as* before accessing the *SelectedIndex* property. 

As I've said in the [other](http://humbletoolsmith.com/2017/03/05/Benefits-of-Pattern-Matching/) [posts](http://humbletoolsmith.com/2017/03/15/Pattern-Matching-and-Tuples/) in this series, this isn't a massive new feature of the language. But I hope that you will agree that this is an incredibly useful feature that will improve your code. If you disagree, please let me know in the comments below. I'd love to hear your perspective. 