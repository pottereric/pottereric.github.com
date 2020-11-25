---
comments: true
date: 2020-10-23 4:00:00
layout: post
slug: upgrading-a-_net-framework-library-to-_net-5
title: "Upgrading a .Net Framework library to .Net 5"
summary: "Let's look at what it takes to upgrade an old .Net Framework class library to .Net 5"
image: 'upgrading-a-_net-framework-library-to-_net-5\lead.png' 
tags:
- DotNet5
---

Next month, .Net 5 will be released. This marks an important evolutionary step for .Net as it switches the primary platform from .Net Framework to .Net Core. Microsoft will upgrade .Net Core 3 and rename it to .Net 5. The version jump signifies that it now supper cedes .Net Framework 4. 

It will be important for all .Net Framework projects to move to .Net 5, or start down the slow road to obsolescence. I've been a part of multiple professional projects that have upgraded from .Net Framework to .Net Core. In this post (which will be the first of several in this series), I want to take an older open source project and upgrade it to .Net 5, documenting all of the steps along the way.

I am going to upgrade the [Biggy](https://github.com/xivSolutions/biggy) library. I choose it because it is roughly 7 years old, making it a more interesting case for upgrading. It is also relatively simple. And I have used it on a side project in the past and I'd honestly like to have to use it on an upcoming side project.

### Installing the Tools ###

I started by installing the preview version of Visual Studio 2019. At the time of this writing, the latest version is 16.8.0 Preview 4. This installed the 5.0.100-rc.2.20479.15 of the .Net SDK. I could have installed the SDK manually and gone through this exercise without Visual Studio. But I also wanted to try out some of the preview features in VS.

[![](/img/posts/upgrading-a-_net-framework-library-to-_net-5/visual-studio-version.png)](/img/posts/upgrading-a-_net-framework-library-to-_net-5/visual-studio-version.png)

### Upgrading the Solution and the Project Files ###

The next step was to upgrade the solution file. In my experience, the easiest way to do this is to copy all of the code to a different folder and create a new solution in the old folder. As long as you use the same file name, your source control history will look like you upgraded the .sln file.

The Biggy solution has multiple projects. I started the conversion by converting the Biggy.Core project, which in turn created the new Biggy solution file.

I made a copy of the Biggy repository. In the primary repository, I deleted all of the files except the README.md file and the .git folder. Then I used Visual Studio to create a new .Net 5 class library. I made sure the solution file was named Biggy.sln and the project file was named Biggy.Core.csproj. I manually edited the csproj file, making the TargetFramework property was set to net5.0.

[![](/img/posts/upgrading-a-_net-framework-library-to-_net-5/target-framework-net50.png)](/img/posts/upgrading-a-_net-framework-library-to-_net-5/target-framework-net50.png)

Then I copied all of the *.cs files from the copy of the project folder to the new project folder. 

### Upgrading the NuGet packages ###

The Biggy.Core project had dependencies on 2 NuGet packages, Newtonsoft.JSON and Inflector. I had to upgrade Newtonsoft to a version that supported .Net Core, but that was easy. Inflector doesn't have a newer version that supports .Net Core. Luckily, the package was only used to pluralize some names. I found a different package named Pluralize.NET.Core that provided the same functionality and it supports .Net Core. Some minor code changes had to be made to switch libraries, but that didn't take to long. 

Once these changes were made, the code compiled and I had a valid .Net 5 assembly. 

### Upgrading the other projects ###

After I got Biggy.Core to compile, I went through the same process with Biggy.Data.Json and the Tests project. I did have to make a minor change to the test project because it would check to see if the output directory was either "Debug" or "Release". By default, .Net Core project put their bin files in directories that end with the platform name. So the debug output was now in "Debug\net5.0" instead of "Debug". 

### Results ###

Overall, moving the first three projects in this solution to .Net Core was pretty easy. If there had been a NuGet package that couldn't have been easily upgraded or replaced that would have made the process more difficult. In the [next post](http://humbletoolsmith.com/2020/11/24/upgrading-configurationmanager-for-_net-5/), I'll try to upgrade Biggy.SqlLite and Biggy.Postges and see if there are larger challenges.