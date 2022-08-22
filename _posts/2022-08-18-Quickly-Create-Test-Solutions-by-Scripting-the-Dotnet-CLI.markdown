---
comments: true
date: 2022-08-18 4:00:00
layout: post
slug: quickly-create-test-solutions-by-scripting-the-dotnet-cli
title: "Quickly Create Test Solutions by Scripting the Dotnet CLI"
summary: "Create a fully configured test solution with a batch file."
image: 'quickly-create-test-solutions-by-scripting-the-dotnet-cli\lead.png' 
tags:
- CSharp 
- FSharp
---

From time to time, I need to create a small C# or F# solution to experiment with a code feature or a library function. Often, what I want to do is create a simple console application and a unit test project that references the console application. This isn't hard to do in Visual Studio, but it feels like it takes too many steps.  

Recently, I read a fantastic new book called Essential F#, by Ian Russel. (You can get [it here](https://leanpub.com/essential-fsharp)) In it, he showed that you could quickly create the setup I described above with the dotnet CLI. It was an idea so brilliantly simple that I'm jealous that I didn't think of it. But I did take it a step further and created a bat file to further automate the process. 

The commands in this script are taken directly from the book. The only modification I've made is to parameterize the solution name and the project name. 

<script src="https://gist.github.com/pottereric/e0ad9760d48d34dfabce7bfb59f5f195.js"></script>

With this script, you could execute something like this command:
```bash
CreateFSharpProject SampleSolution SampleProject
```
This would create a new Solution named SampleSolution. It would contain two projects F#, SampleProject and SampleProjectTests. The test project already has a reference to the primary project and is ready to execute the tests with FsUnit. 

I created a similar script file for C# and MSTest. 

<script src="https://gist.github.com/pottereric/03b83ef8a950eaab91b256e83044eab1.js"></script>

With these scripts, you can quickly create solutions with the unit test project already configured. That way, you can jump right into the code experiment you want to run. 

You can take this concept and modify it to create whatever kind of project and unit test project you want. Hopefully, it is a simple little time saver for you.
