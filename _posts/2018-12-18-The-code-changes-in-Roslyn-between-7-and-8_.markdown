---
comments: true
date: 2018-12-18 4:00:00
layout: post
slug: the-code-changes-in-roslyn-between-7-and-8_
title: "The code changes in Roslyn between 7 and 8."
summary: "A look at home much had to change inside the compiler for the latest version."
image: 'the-code-changes-in-roslyn-between-7-and-8_\lead.png' 
tags:
- C#
- NDepend
---

For the second year in a row, Matt Groves is coordinating the [C# Advent Calendar](https://crosscuttingconcerns.com/The-Second-Annual-C-Advent). It is a fantastic collection of posts on a wide variety of C# topics. I strongly encourage you to check out the other posts in series. For my entry, I wanted to take a look at the C# codebase behind the C# compiler.


I've been fascinated with the Roslyn codebase ever since it was announced. With C# 8 now released in a preview state, I was curious to know how much C# code it took to update the compiler from C# 7.0 to 8.0. 

I cloned the Roslyn repository to my local machine. Then I used NDepend to compare the current state of the master branch (as of 12/17/18) to the branch named 'dev15.0.x'. This is the branch that shipped with Visual Studio 15.0, better known as Visual Studio 2017. This should be the first released version of C# 7.0. It will be the baseline for my comparison. For this exercise, I wanted to focus on the compiler itself, so I only looked at three projects:

1. CSC.exe - the command line shell for the compiler
2. Microsoft.CodeAnalysis.dll - the core of the compiler
3. Microsoft.CodeAnalysis.CSharp.dll - the C# specific part of the compiler

This will admittedly leave out the changes that had to be made in the framework and additions to the unit test suite. But I am choosing to focus on the compiler.

[![](/img/posts/the-code-changes-in-roslyn-between-7-and-8_/il_instruction_count.png)](/img/posts/the-code-changes-in-roslyn-between-7-and-8_/il_instruction_count.png)

NDepend reports that there are an additional 141,111 IL instructions. This represents 11.3% of the overall code base.  


[![](/img/posts/the-code-changes-in-roslyn-between-7-and-8_/types_methods_count.png)](/img/posts/the-code-changes-in-roslyn-between-7-and-8_/types_methods_count.png)

Looking at the changes at a more granular level we see there are 499 new types and 3,260 new methods. While some of the types seem to have come from refactoring, many of them are directly related to the new language features. 

[![](/img/posts/the-code-changes-in-roslyn-between-7-and-8_/new_types.png)](/img/posts/the-code-changes-in-roslyn-between-7-and-8_/new_types.png)

Here we can see some of the types that are directly related to new language features, like Ranges and functionality about nullability. 

Here is the most impressive statistic that NDepend reports.

[![](/img/posts/the-code-changes-in-roslyn-between-7-and-8_/method_complexity.png)](/img/posts/the-code-changes-in-roslyn-between-7-and-8_/method_complexity.png)

With all of the changes, the average method complexity basically remained flat. In most code bases, an 11% increase in functionality would lead to a large increase in complexity, if not technical debt. Here, the team has managed to add the new functionality without making the code messy. 

There are some methods that got more complex out of necessity. For example, there is a method that returns the text of each kind of syntax item. With the additon of a few operators, it must get more complex. 

## Take Aways ##

Far too many code bases get messier and more complex as they evolve. But the C# compiler is a great example that proves that code can remain clean as it grows. The challenge here is that in your code base, you need to continuously work to keep the code clean and simple. Don't settle for unnecessary technical debt and code rot as a code base ages. Work to keep in clean.
