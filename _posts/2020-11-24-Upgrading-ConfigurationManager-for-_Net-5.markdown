---
comments: true
date: 2020-11-24 4:00:00
layout: post
slug: upgrading-configurationmanager-for-_net-5
title: "Upgrading ConfigurationManager for .Net 5"
summary: "Using old config files in .Net 5 applications"
image: 'upgrading-configurationmanager-for-_net-5\lead.png' 
tags:
- DotNet5
---

In [my previous post](http://humbletoolsmith.com/2020/10/23/upgrading-a-_net-framework-library-to-_net-5/), I described my efforts to upgrade an older .Net Framework code base to .Net 5. The initial effort was to get some class libraries moved over. Those libraries didn't have many external dependencies. This post will describe what it took to upgrade other class libraries in the same solution that required dependency changes, many System.Configuration.ConfigurationManager.

While the core Biggy library simply stores objects in JSON files, additional Biggy libraries that store objects as JSON in SQLLite, Postgres, and Azure Blob Storage. There are required Nuget packages for all 3 and luckily for me, all 3 have updated versions that run on .Net 5. So those upgrades were easy.

What was slightly more complex was getting the connection strings for SQLLite and Postgres. The Biggy project started in 2014, and as was considered best practice at the time, the connection strings were stored in app.config files and were accessed with System.Configuration.ConfigurationManager.

With the advent of .Net Core, the best practice is to store settings and connection strings in appsettings.json files. And in a future blog post, I'll upgrade Biggy to use them. But at this stage in the conversion, I wanted to see if I could continue to use the app.config files.

When I first tried to compile the code, I got a few errors because the compiler couldn't find the ConfigurationManager type. This because it has been removed from the core set of libraries. While .Net Framework included a plethora of classes in its core set of libraries, .Net Core (and now .Net 5) take a much more modular approach. This makes the core set of libraries much smaller. While the Configuration classes aren't in the core set of libraries, like many other .Net 5 classes, they are readily available as NuGet packages. 

[![](/img/posts/upgrading-configurationmanager-for-_net-5/ConfigurationManagerNugetPackage.png)](/img/posts/upgrading-configurationmanager-for-_net-5/ConfigurationManagerNugetPackage.png)

I installed the NuGet package for System.Configuration.ConfiguraitonManager (version 5.0). Right away, the app was able to use the connection strings to connect to the databases successfully.

While I wouldn’t suggest using this NuGet package for new .Net 5 projects, if you upgrade older projects that use app.config or web.config files, this package will get you up and running.




