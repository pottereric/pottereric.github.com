---
comments: true
date: 2014-04-30 14:30:00
layout: post
slug: What is so exciting about Roslyn?
title: What is so exciting about Roslyn?
summary: 'What is so exciting about Roslyn?'
image: 'The-right-size-wrench\wrenches.thin.jpg'
tags:
- Roslyn
---

I had someone ask me recently why I am so excited about Roslyn. It is a fair question because while Roslyn is an amazing technology, all of the benefits are not immediately obvious. 

## What is it ##

If you are not familiar, Roslyn is the code name for Microsoft's next generation .NET compilers. But more than that it is a library that exposes the compiler's internal data structures and a framework that enables customization of the compilation process. This is a radical departure from the current C# and VB compilers, and the vast majority of all compilers. Most compilers are black boxes. Code goes in one side and an executable comes out the other side. At a conceptual level, a user might know what is happening under the hood, but there is no access to the inner workings. 

Roslyn changes that. Roslyn give you the ability to take a source file as input, but get access to the syntax tree once it has been parsed. It gives you the ability to view the semantic information about a syntax node once it has been generated. Having analyzed the source, you have the ability to alter the IL before it is generated.

## So What ##
But the question remains. So what. Why is this so exciting? With direct access to the syntax tree and its semantic information, we can pro grammatically understand our code easier than ever before. As programmers, our code is our poetry. It is the blueprint for our designs. It is how we communicate with the machine. It is one way that communicate with other programmers. 

One of the great things about unit tests is that they allow us to test our code with code. In a similar way, Roslyn allows us to understand and analyze our code with code. That is very powerful.

None of the functionality come out of the box, you have to write it. Conveniently, you are very good at writing software. So you have to find an itch and then scratch it with Roslyn. You can create tools to make the development process easier. If you share those tools, it benefits our entire community. Creating tools is fundamentally [what we do](http://www.cs.unc.edu/~brooks/Toolsmith-CACM.pdf). With Roslyn, we can create tools for ourselves.

Even if you don't use Roslyn to create tools, you will benefit from it. Roslyn will enable Microsoft to more easily make improvements both to the C# and VB languages and to the Visual Studio experience. Commercial tools also have access to Roslyn, which will allow then to create more and better tools. And it will allow them to do it faster.

As an example of what you code do, [Joe Hummel](http://blog.joehummel.net/) did a great presentation at the Chicago Code Camp where he created a [Visual Studio extension](http://joehummel.net/downloads.html) that would generate a compiler warning if there was code that had an empty catch block. It could have been easily altered to generate a compiler error. It also had the ability to suggest a code fix. So if you had an empty catch block, you would get a tool tip that add a throw to the catch block for you.

In the Object Oriented Design class I taught this semester, I had my students use Roslyn to look at C# source files and gather the number of statements and max nesting depth of each method. Using this information they could suggest which methods in the file were too complex and in need of refactoring. 

That example highlights one of those inception moments Roslyn enables. The code can analyze itself. The rabbit hole gets deeper when you realize that Roslyn can compile itself.

So let's get back to the original question, why I am so excited about Roslyn? I am excited about the tools you and I are going to build with it.
