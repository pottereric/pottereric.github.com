---
comments: true
date: 2016-08-29 14:30:00
layout: post
slug: Driving-Canopy-Tests-with-TypeProviders
title: Driving Canopy Tests with TypeProviders
summary: 'Driving Canopy Tests with TypeProviders'
image: 'Driving-Canopy-Tests-with-TypeProviders\canopylink.jpg'
tags:
- Canopy
- FSharp
---


One of the most amazing features in F# is [Type Providers](https://docs.microsoft.com/en-us/dotnet/articles/fsharp/tutorials/type-providers/index). They allow you to access data sources in incredibly easy ways. You can query data from databases, read data from CSV files, or consume JSON data from an API.  I'm not going to go into depth here on Type Providers, but if you are unfamiliar with them, you should go [check them out](http://fsharp.github.io/FSharp.Data/index.html). 

Often times when I am writing Canopy tests, I want to validate that some data from the database is being displayed on the screen. So what I need to do is get the data from the database and use it in a Canopy test. 

To use a TypeProvider for data retrieval, the first thing you will need to do is include the FSharp.Data.TypeProviders assembly from NuGet. After that, this is all of the code that you need to start getting data.

<script src="https://gist.github.com/pottereric/c9ede1854d5c89dfa1650e5096331388.js"></script>

That is it. There is nothing else to do. You have strongly typed classes based on the data in your data source. 

In this example, I am using the data from the [Crisis Checkin](http://www.htbox.org/) database. Now that I have queried the list of disasters, I could easily right a test that ensures that all of the disasters are listed on the site. Or I could right tests that ensure that volunteers can register for disasters that are currently open. 

Driving tests from the database allows the tests to use relevant information that stays up to date with the web application under test. There is no need to maintain a separate data source for the test data, it can easily directly from the database. 
