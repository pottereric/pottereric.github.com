---
comments: true
date: 2020-12-18 4:00:00
layout: post
slug: upgrading-old-csharp-to-csharp-9-init-only-setters
title: "Upgrading Old C# to C# 9: Init Only Setters"
summary: "How can init only setters be used to make C# 9 more clearly express write-once behavior?"
image: 'upgrading-old-csharp-to-csharp-9-init-only-setters\lead.png' 
tags:
- C#
- C#9
---

This is my contribution to the fantastic series of blog posts in this year's [C# Advent Calendar](https://www.csadvent.christmas/). Please check out the rest of the posts for more great content.

-----

In my past [two](http://humbletoolsmith.com/2020/10/23/upgrading-a-_net-framework-library-to-_net-5/) [posts](http://humbletoolsmith.com/2020/11/24/upgrading-configurationmanager-for-_net-5/), I've looked at upgrading an older C# code base to .Net 5. In this post I'm going to start looking at modernizing the code in that library to use C# 9. Specifically, I'm going to look at the benefits of using Init Only Setters.

In the Biggy code base, there is a class named DbColumnMapping that is a prime candidate for init only setters. The class has properties that hold metadata about columns. Obviously, there is some data, like the table name, that never needs to change. But it is nice to be able to set the value from outside the class. 

Here is a place in the class named SqliteDbCore where an object initializer is used to set the TableName property. 

[![](/img/posts/upgrading-old-csharp-to-csharp-9-init-only-setters/initializer.png)](/img/posts/upgrading-old-csharp-to-csharp-9-init-only-setters/initializer.png)

You can see how useful it is to be able to set the table name in the object initializer. This could also be done by creating a new constructor for DbColumnMapping, but then the constructor would need to be created and maintained. That wouldn't be hard, but it would be for work. 

In the previous version of the code, the property had a public setter. This functions correctly, but it means that the property can now be legally set at any time, when really the property should be effectively read-only. 

This is why C# 9 introduces Init Only Setters. Instead of using the "set" keyword, the property is defined with the "init" keyword.

[![](/img/posts/upgrading-old-csharp-to-csharp-9-init-only-setters/diff.png)](/img/posts/upgrading-old-csharp-to-csharp-9-init-only-setters/diff.png)

This allows the property to be set in the object initializer, specifically in this case, in the SqliteDbCore class. But the property cannot be changed after the object creation is done.

This isn't a feature that will radically change how you write code. It is a feature that will help you clearly express your design decisions to the compiler and to future maintainers of your code.