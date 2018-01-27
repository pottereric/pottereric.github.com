---
comments: true
date: 2018-01-27 4:30:00
layout: post
slug: making-canopy-tests-repeatable-with-respawn
title: Making Canopy Tests Repeatable With Respawn
summary: 'One of the challenges of creating integration tests is making them repeatable. Respawn can help.'
image: 'Making-Canopy-Tests-Repeatable-With-Respawn\CanopyAndRespawn.png'
tags:
- Canopy
---

Creating integration tests is a great way to validate the functionality of a web application, from the JavaScript all the way to the database. One of the challenges comes from the fact that data is being persisted to the database. In some cases, this prevents the tests from working properly when the test run is repeated.

As an example, let's say that we have a test that creates a user account with a unique email address. The first time we run the test suite, the test will pass because the email address is unique. The second time we run the test suite the test will fail because the account can't be created a second time. The test would fail even though the software was working correctly. False failures are always a headache with integration tests. So we want tools to solve this problem.

Recently, a library named [Respawn](https://github.com/jbogard/Respawn) was released for situations just like this. It was created by Jimmy Bogard, who is also the creator of popular libraries like [AutoMapper](https://github.com/AutoMapper/AutoMapper) and [MediatR](https://github.com/jbogard/MediatR). Respawn will reset your database back to a known base state. It doesn't this by intelligently deleting data out of your database. It is fast, so you can reset your database multiple times within a test suite. You can read the [full description](https://lostechies.com/jimmybogard/2015/02/19/reliable-database-tests-with-respawn/) here. In this post, I specifically want to explore how Respawn works with Canopy.

## Using Canopy and Respawn Together

Respawn was written with test runners like XUnit and MSTest in mind. But I believe it will work well with [Canopy](https://lefthandedgoat.github.io/canopy/). Respawn and Canopy are both .Net assemblies, so they can be seamlessly integrated into the same project. I assume that Respawn could also be used with other .Net based web integration test frameworks, but I am primarily interested in Canopy.

I'm a [huge fan of Canopy](https://channel9.msdn.com/Blogs/Technology-and-Friends/tf398). I think it is a beautiful way to create automated integration tests for web applications. The fact that you get to write the tests in F# makes it [even](http://humbletoolsmith.com/2016/08/29/Driving-Canopy-Tests-with-TypeProviders/) [better](http://humbletoolsmith.com/2016/08/19/Validating-List-Sorting-with-Canopy/). But it doesn't have a built in way to reset your database back to a known state. Luckily, it is easy to use Respawn from within your Canopy test suite. 

Like Canopy, Respawn is a NuGet package. So it is trivial to include it in your project. Once it is included, you just need to do two things:
1. Declare which tables in your database you don't want to delete.
2. Determine where in your test suite you want to reset the database.



### Declaring the tables that shouldn't be reset

To start using Respawn, you need to create an instance of a Checkpoint. The Checkpoint object has a property name TablesToIgnore that tells the checkpoint which tables shouldn't be deleted. All other tables will have their data deleted. Respawn will use the foreign keys to figure out which tables need to be cleared first. The property is an array of strings. Assigning it in F# looks like this:    

<script src="https://gist.github.com/pottereric/0301d13ae8463df3961f21505b3f4410.js"></script>

For this example, I [created a project](https://github.com/pottereric/CanopyRespawnDemo) that performs a simple test on the open source [CrisisCheckin](https://github.com/HTBox/crisischeckin) project. There are a number of tables that need to be populated in order for the application to work properly. So I included them in the list of tables to ignore.

### Resetting the database

With the checkpoint created, you just need to call it's Reset method to set the database back to the base state. The Reset method takes a connection string as a parameter. It relies on the fact that the integration test application can connect to the database and delete data from it. So if your integration tests run against a staging server where you don't have direct access to the database, this solution won't work for you. 

In Canopy, we have methods that get called at known times that are great places to reset the data. The "once" function gets called one time at the beginning of each test context in your test suite. It is a useful place to call Reset.

<script src="https://gist.github.com/pottereric/487bf0ca5c82d622cc232d222af556e6.js"></script>

If you want to reset the database right before every test in a test context, you could you use the "before" function. In this scenario, the quickness of Respawn would be very useful. If you wanted to reset the data after each test or at the end of a test context, you could use Canopy's "after" or "lastly" functions.

## Conclusion

I put together an exploratory project using Canopy and Respawn together. You can see it [here](https://github.com/pottereric/CanopyRespawnDemo). If you want to run it, you will need to clone the CrisisCheckin repo and run it locally. I was pleased with how smoothly the two libraries worked together. I was also pleased with how easy it was to use them to create integration tests that are repeatable and reliable.
