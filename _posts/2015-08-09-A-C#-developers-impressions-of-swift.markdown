---
comments: true
date: 2015-08-09 14:30:00
layout: post
slug: C# Developer's Impression of Swift
title: C# Developer's Impression of Swift
summary: 'My First Impressions of the programming in Swift'
image: 'impressions-of-swift\code.png'
tags:
- C#
- swift
---



 As part of our continuous learning efforts at Aptera, we had a competition to see who could come up with the best implementation of Fizz Buzz in Swift. This was my first time coding in Apple's new language. 

## The Simple Solution ##

At the beginning of my career, I was a C / C++ developer. So for my first implementation, I fell back on those roots. 

<script src="https://gist.github.com/pottereric/aa08dbda44ed217f8975.js"></script>
[See it in action](http://swiftstub.com/493396526/?v=gm)

The first thing worth noting is that Swift is a low ceremony language. I didn't have to implement a Main method. Whatever code is outside of other blocks gets executed. In this, case, just line 24. The next noteworthy thing for devs that primarily work in C based languages is that the semi-colons are optional. I included it on line 9 and omitted it on line 12. Both execute properly. While Swift is an object oriented language, it has functional elements. The first hint of that is on line 1, which declares a member with the "let" keyword. This makes it immutable, or a constant. Mutable variables are declared with the "var" keyword, demonstrated on line 9. In both of these declarations, you can omit the type specification. This is because the compiler can imply the type for the initial assignment. 

This solution functions properly, but the implementation didn't make much use of the more interesting parts of the Swift language. It is essentially a C solution that I wrote in a .swift file.

## Using a Swift Switch Statement ##

The first language feature I wanted to explore was the switch statement. Swift makes use of pattern matching in it's switch statements 

<script src="https://gist.github.com/pottereric/7a477ce241dadbd9f3de.js"></script>
[See it in action](http://swiftstub.com/227316875/?v=gm)

In this solution, the switch statements operates on the variable i. It matches using the wild card pattern "_" and a where clause. In this example, it is uninteresting because all of the cases match on the wild card. But you can see how it would be useful to match on a value and a condition. This could flatten out nested logic into a single selection statement.

Of lesser importance is the fact that the case blocks don't require a break statement. The language assumes that you only want to execute on block. If you want to execute another block, you have to insert the "fallthrough" keyword. Another nice feature is the built in support for ranges. On line 4, I declare a range from 1 to max and iterate over it.  

Another nice facet of the switch statement is that a single case can match multiple values. 

<script src="https://gist.github.com/pottereric/3976a4ea9fbfeb68b516.js"></script>
[See it in action](http://swiftstub.com/960237223/?v=gm)

In this case, lines 9 and 11 match multiple values.

To really make use of pattern matching, I needed to move to a more interesting solution. 

## Tuples and Pattern Matching ##

<script src="https://gist.github.com/pottereric/8f58766ddcba6418b78a.js"></script>
[See it in action](http://swiftstub.com/694157572/?v=gm)

This solution makes use of on my favorite Swift language features, Tuples. C# has tuples as a generic class, but Swift has them as a language construct. This allows for some really elegant usages.  

The first function returns a tuple of bool, bool indicating whether or not the value is a multiple of three and/or fire. Now the switch statement on line 7 can pattern match the tuple. 

Another thing to note from this solution is that types are always declared with a colon and a type name following the identifier. On line 1, I declared the parameter type as an int. The return type of the function is the tuple of bool, bool. Declaring the return type with an arrow ("->") was new to ne, but I found it very intuitive. 

## Closures ##

<script src="https://gist.github.com/pottereric/5e89a6e6c9be1ceb8580.js"></script>
[See it in action](http://swiftstub.com/161998270/?v=gm)

As I mentioned before, Swift has functional elements. One of the hallmarks of functional languages is that they have functions as first class elements. So you can assign functions to variables and pass them as arguments to other functions. 

One of the variations on FizzBuzz is to return Fizz or Buzz for numbers that contain 3 or 5 instead of being multiples of 3 or 5. Another variation is to parameterize which numbers to check for instead of hard coding 3 and 5 and paramaterizing the words instead of hard coding Fizz and Buzz. 

In this solution I support both of those cases by passing in the text to return and passing in anonymous functions to check the numeric values. Swift calls these types of functions closures. I updated ListFizzBuzzResults to accept two closures which find the target values. ListFizzBuzzResults passes those same closures to the method named IsFizzBuzz. IsFizzBuzz performs the checks for the target values.

This allows me to control how the program executes by passing different closures to ListFizzBuzzResults. On line 25 I declare and pass closures that check for multiples of three and multiples of five respectively. On line 28 I declare and pass closures that check for values containing 3 or 5. I can have either functionality simply by changing one line. I could easily have some combination of the two cases as well.

Declaring the closures is very terse. You wrap the code you want in the closure in braces. You identify the arguments with a dollar sign and their position number. For example, you use "$0" to identify the first argument. 


To make this solution follow the functional paradigm, I also changed line 8 from a for statement to a map. I put the switch statement in a closure which gets passed as an argument to map. In this case I use the other closure syntax that allows me to define the parameter names instead of just using $0. 

## Overall Impressions ##

Having only spent a few days with it, I really enjoyed the Swift language. The syntax is terse, but sensible. It has many of the features of the most modern languages without felling entirely foreign. It allowed me to mix some functional features into object oriented code. 

I suppose the highest praise that I can give it is that I hope to write more of it in the future. 