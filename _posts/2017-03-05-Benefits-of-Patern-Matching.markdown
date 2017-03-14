---
comments: true
date: 2017-03-05 14:30:00
layout: post
slug: Benefits of Pattern Matching
title: Benefits of Pattern Matching
summary: 'Pattern Matching'
image: 'Benefits-of-Pattern-Matching\MainPage.jpg'
tags:
- PatternMatching
- C#
---

As someone who dabbles in F#, I was excited when I heard that C# was getting Pattern Matching. In this post I want to look at why it is so beneficial. 

The three basic control flow mechanism available in all programming languages are selection, iteration, and calling subroutines. In same way that a *foreach* loop is an evolutionary step for iteration, pattern matching is an evolutionary step for selection. It isn't a ground breaking new paradigm like async/await or Linq, but it is something that will be useful at a fundamental level. The *foreach* loop doesn't allow you to do things that you couldn't do with a *for* loop or a *while* loop, it allows you to do them faster and with cleaner code. In the same way, pattern matching won't allow you to do things you could do with *if* statements, it just enables you to write them better.

Here is an example from the Roslyn repository. As of this writing, you could find the source file [on GitHub](https://github.com/dotnet/roslyn/blob/master/src/Features/Core/Portable/ConvertNumericLiteral/AbstractConvertNumericLiteralCodeRefactoringProvider.cs).

It is code that looks for possible refactorings where [digit separators](https://blogs.msdn.microsoft.com/dotnet/2016/08/24/whats-new-in-csharp-7-0/) could be used. So it would recommend digit separators for decimal constants with more than 3 digits and digit separators for binary and hexadecimal constants with more than 4 digits.  

<script src="https://gist.github.com/pottereric/2782f4e7bb1b25aef17bb50d29f7f9c7.js"></script>

The code switches on an enum that describes the type of numeric constant. Each case statement has a *when* clause that only allows selection of the current case when a length requirement is met. The combination of the enum type and the *when* clause make up the pattern. 

This could all be done with *if* statements, but it would be more code. The benefit of using pattern matching in this is that it case makes the code cleaner and more readable. 



