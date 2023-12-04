---
comments: true
date: 2023-12-03 4:00:00
layout: post
slug: dissecting-csharp-ranges
title: "Dissecting C# Ranges"
summary: "Learning about C# ranges by looking inside."
image: 'dissecting-csharp-ranges\lead.png' 
tags:
- C#
---
This post is part of [2023 C# Advent](https://www.csadvent.christmas/)! Be sure to check every day for new posts from the .NET community!

Recently, I was teaching C# to a group of developers. When I got to the topic of ranges, I was surprised at how much nuance there was. In this post, I don't want to go into all of the features of ranges. That is covered in other places. I want to look at the structure of ranges to see that we can learn about them.

Grab a scalpel, lets slice one open. 

Here is an example of a simple range. In case the range is accessing an array of numbers from index 3 to the index 3 from the end.

[![](/img/posts/dissecting-csharp-ranges/01 The Line of Code.jpg)](/img/posts/dissecting-csharp-ranges/01 The Line of Code.jpg)

This works because integer arrays, like many other collections, have a range access property. You can easily add range access to your types by creating a property named 'this' that takes a Range as a parameter. 

[![](/img/posts/dissecting-csharp-ranges/01A Range Access.png)](/img/posts/dissecting-csharp-ranges/01A Range Access.png)

But what exactly is a Range? As you can see from its definition pictured below, it is a struct whose primary pieces of data are a start value and an end value. 

[![](/img/posts/dissecting-csharp-ranges/03 Definition of Range.jpg)](/img/posts/dissecting-csharp-ranges/03 Definition of Range.jpg)

But the data type of start and end isn't int, it is Index. So, what is an index? It is a struct whose primary pieces of data are a value and flag indicating whether or not the value is measured from the end of the collection. 

[![](/img/posts/dissecting-csharp-ranges/02 Definition of Index.jpg)](/img/posts/dissecting-csharp-ranges/02 Definition of Index.jpg)

Going back to the original line of code, we can see that the caret is the indicator to the compiler whether or not the fromEnd property on the Index is true.

We can use the Syntax Visualizer in Visual Studio to see how the compiler thinks of Ranges. Range Expressions (1) are wrapped in a BracketedArgumentList. They contain the start expression, the aptly named DotDotToken, and the end expression. In this case, the start expression is a NumericLiteralExpression(2) and the end expression is a IndexExpression(3). As you can see, the IndexExpression contains a CaretToken and a NumericLiteralExpression. 

[![](/img/posts/dissecting-csharp-ranges/04 Range Expression Syntax.jpg)](/img/posts/dissecting-csharp-ranges/04 Range Expression Syntax.jpg)

Why doesn't the start token need to be an IndexExpression? While the compiler can do all kinds of tricks, it helps that the Index type contains an implicit conversion from int to Index.

[![](/img/posts/dissecting-csharp-ranges/05 Index Implicit Conversion From Int.jpg)](/img/posts/dissecting-csharp-ranges/05 Index Implicit Conversion From Int.jpg)

We have yet to begin to dig into the functionality of Ranges, but I hope this look at their structure gives us a little more understanding of how they work.

