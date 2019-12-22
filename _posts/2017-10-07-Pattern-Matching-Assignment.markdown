---
comments: true
date: 2017-10-07 14:30:00
layout: post
slug: pattern-matching-and-assignment
title: Pattern Matching = Conditional and Assignment
summary: 'Combining the condition with the assignment is the brilliance of pattern matching.'
image: 'pattern-matching-and-assignment\PatternMatchingFunnelLead.png'
tags:
- PatternMatching 
- CSharp
---

I've been in love with pattern matching in C# since I first heard it was going to be added to the language. I had used it in F# and was excited to use it is C#. In a conversation I had this week I realized something important that I had known about pattern matching, but I had never articulated it. One of the most powerful things about pattern matching is that it cleanly combines a conditional statement and an assignment statement into a single line of code.

Let's look at the following code taken from the Entity Framework Core [code base](https://github.com/aspnet/EntityFrameworkCore/blob/3e0d7249a1196e934249d440d2e6de028096be6f/src/EFCore.Relational/Query/Sql/DefaultQuerySqlGenerator.cs)

<script src="https://gist.github.com/pottereric/e79634c1963737fddb3d3fcb829d0fe3.js"></script>

On line 3 the code will switch on the expression variable. If the expression is an instance of ColumnExpression, the statement on line 5 will evaluate to true, but it will also assign the variable named columnExression. The variable named columnExpression will have a type of ColumnExpression and will be assigned the value stored in expression. Similar things happen on lines 7 and 9 if the type of expression is ColumnReferenceExpression or AliasExpression. 

The magic here is that in a concise but readable statement, the type is evaluated and the variable is assigned. This makes the code much cleaner than if the type check and the expression were in separate statements for each possible type. Also noteworthy is that there is no need for a null check because a if expression is null, the switch statement will match on the default case. (If it were present, it would match on "case null:".)

So the pattern matching is C# combines the functionality of "is" and "as" into one statement. It can be used directly in a "switch" statement. It resembles a more powerful version of TryParse in that it can both evaluate the type and do the assignment. It also resembles a regex in how it can determine the validity of the match and pick values out of the input. Of course, TryParse and regex only work on strings where pattern matching can work on any type.

[![](/img/posts/pattern-matching-and-assignment\PatternMatchingFunnel.png)](/img/posts/pattern-matching-and-assignment\PatternMatchingFunnel.png)

Pattern matching combines aspects of all of these constructs into one powerful feature. 
