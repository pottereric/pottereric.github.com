---
comments: true
date: 2018-04-05 4:00:00
layout: post
slug: t4-csharp_s-little-known-code-generator
title: "T4: C#'s Little Known Code Generator"
summary: "Generating Text Programmaticly"
image: 't4-csharp_s-little-known-code-generator\lead.png' 
tags:
- CSharp
---

The thing that I want to talk about in this post is not something new. It is something that has been available to Visual Studio developers for a few years now. It is not something that I see many people using. But it is something that I find to be very useful. I am talking about T4 templates. 

T4 templates allow you to generate text in a similar way to how Razor pages allow you to generate HTML. It is a markup language that mixes C# with text. The text that is generated could be C# code or JSON. It could also be any text that you need to generate from some other data source.

Entity Framework made heavy use of T4 templates back in the Model-First paradigm. It would use the XML model of the database as the source and it would generate C# code with the T4 templates. If you wanted to alter the code that EF generated from the model, you could alter the T4 files. 

This power is available to you for your code generation needs. You need some data source, which could be anything that is available to you with C#. As long as there is an algorithmic way to go from the data source to the output, you can generate it with T4. 

It is simple to get started with T4. In an existing C# project, use the Visual Studio tools to add a new item. 

[![](/img/posts/t4-csharp_s-little-known-code-generator/body.jpg)](/img/posts/t4-csharp_s-little-known-code-generator/body.jpg)

On the Add New Item dialog you can search for T4 and you will see at least 2 templates available. I have the [Tangible T4 Visual Studio Extension](http://t4-editor.tangible-engineering.com/T4-Editor-Visual-T4-Editing.html) installed, so there are 4 additional templates. 


### Text Template ### 
The Text Template is an item that will generate output right in your Visual Studio project every time the project is built. Effectively, these templates get transformed at compile time. They are generally used to generate code that will be compiled into the current project. This is the model that Entity Framework used. 

### Runtime Text Template ###
When you create an item with the Runtime Text Template, you create a class that can transform text when the program is executed. It is designed for scenarios where the output will live outside the project. 

I build this blog with Jekyll, a static site generator. Every time I start a new post I have to create a new markdown file that follows certain conventions. I created a small C# project that uses a Runtime Text Template that takes some metadata and creates a markdown file with much of the necessary information already filled in. 

In the past I have also Runtime Text Templates to read data from a database and generate C# static mock data for use in unit tests. 

Software development involves manipulating a lot of text files. Anytime some of that can be automated means that you can get to your high-value work faster. If you haven't explored T4 Templates, it is something I recommend you add to your toolbox. 


[Tutorial for working with Text Templates.](https://docs.microsoft.com/en-us/visualstudio/modeling/design-time-code-generation-by-using-t4-text-templates)

[Tutorial for working with Runtime Text Templates.](https://docs.microsoft.com/en-us/visualstudio/modeling/run-time-text-generation-with-t4-text-templates)


