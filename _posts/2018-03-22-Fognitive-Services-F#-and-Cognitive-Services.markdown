---
comments: true
date: 2018-03-22 04:30:00
layout: post
slug: F#-and-Cognitive-Services
title: "Fognitive Services: F# and Azure Cognitive Services"
summary: "Accessing Microsoft's powerful machine learning tools with an F# service call."
image: 'Fognitive-Services-FSharp-and-Cognitive-Services/FognitiveServices.png'
tags:
- FSharp
- CognitiveServices
- Canopy
---


Machine Learning is revolutionizing how we think about processing data. But machine learning algorithms can have a steep learning curve. Luckily, Microsoft has released an easy way to access very powerful machine learning models through [Azure Cognitive Services](https://azure.microsoft.com/en-us/services/cognitive-services/). They expose the power of machine learning through the ease of calling a REST API.

Microsoft provides good [samples](https://docs.microsoft.com/en-us/azure/cognitive-services/computer-vision/) for calling into the API in C#, Java, JavaScript, PHP, Python, and Ruby. But I wanted to try it from F#. At the MVP Summit, I talked with [Reed Copsey](https://github.com/ReedCopsey) about this idea and he suggested I that I create an F# wrapper for the API. The wrapper could allow someone to call into Cognitive Services using idiomatic F# code. Thus the idea for [Fognitive Services](https://github.com/pottereric/FognitiveServices/) was born.

With help from Reed and [Ryan Riley](https://twitter.com/panesofglass), I created the start of this project. It is built on the existing NuGet package for Cognitive Services .NET SDK. We started with the C# sample code and did a basic translation of it into F#. Then we refactored it to be idiomatic F# code. For example, the API now takes an F# list of tuples instead of a C# list of a custom data structure. This means that the API integrates smoothly with the other F# language tools like piping and pattern matching. Ryan and I recorded a [screencast](https://www.youtube.com/watch?v=V6URf4AnPGs) while we did part of this refactoring. 

The GitHub repo contains some sample apps for each API. But I also put together a slightly more interesting demo project. The Cognitive Services Text API has the ability to pick out key phrases from a block of text. There is a wrapper in Fognitive Services for this in FognitiveServices.Text and there is a [NuGet package](https://www.nuget.org/packages/FognitiveServices.Text/) for it. I thought it would be interesting to use [Canopy](http://lefthandedgoat.github.io/canopy/) to screenscrape the session list from the [StirTrek](https://stirtrek.com/) conference page and pick out the key phrases from each session. This turned out to be incredibly easy. The entire project is available on [GitHub.](https://github.com/pottereric/StirTrekKeywordAnalyzer) Here is the meat of the code.

<script src="https://gist.github.com/pottereric/e5e00bca3f7cc8ca61790616d2a483b6.js"></script>

All of the real work is done in the analyzeStirTrekTags function. Lines 9 and 10 load up the page in the browser. Line 12 initializes the Cognitive Services client. Lines 15 and 16 scrape the session titles off of the web page. The list of titles is seamlessly piped into the FognitiveServices API call on line 17 which returns the results. Line 19 prints the results. 

This easy integration between two F# libraries was one of the main goals behind Fognitivie services. It combines the ease and power of Cognitive Services with the power and elegance of F#. 




