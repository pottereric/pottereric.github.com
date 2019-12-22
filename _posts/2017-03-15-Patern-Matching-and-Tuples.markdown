---
comments: true
date: 2017-03-15 14:30:00
layout: post
slug: Pattern Matching and Tuples
title: Pattern Matching and Tuples
summary: 'Pattern Matching and Tuples'
image: 'Benefits-of-Pattern-Matching\MainPage.jpg'
tags:
- PatternMatching
- CSharp
---

As I discussed in my [previous post](http://humbletoolsmith.com/2017/03/05/Benefits-of-Pattern-Matching/), pattern matching in a new feature in C# 7.0 that provides a more sophisticated way to write selection statements. The situations where sophisticated selections statements more necessary is when selecting on multiple criteria. Often this is seen in other languages when matching against tuples. In an [older post](http://humbletoolsmith.com/2015/08/09/C-Developer's-Impression-of-Swift/), I looked at how Swift uses tuples and pattern matching and used the FizzBuzz problem as a solution. Since C# 7.0 also introduced a better syntax for tuples, I thought would be helpful to revisit the solution, this time in C#. 

<script src="https://gist.github.com/pottereric/d2c805ee3b0adb0c9085589aecceae89.js"></script>

In the code, the method IsMultipleOf3or5 returns a tuple made of two bools. In this instance, the members of the tuple are given names to make them more readable. This is a big improvement over the old C# tuples that had to be named Item1 and Item2. 

The result of IsMultipleOf3or5 is the value that is the subject of the switch statement. Each case statement uses a pattern that names the variable that is being switched. In each case the variable name is status. The *when* clause then uses the property names defined in the tuple to filter the selection. 

Like I said in the previous post, this logic could certainly be implemented with *if* statements, but the new pattern matching logic makes the code cleaner and easier to read.





