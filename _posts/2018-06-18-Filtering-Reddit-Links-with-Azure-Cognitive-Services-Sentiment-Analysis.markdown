---
comments: true
date: 2018-06-18 4:00:00
layout: post
slug: filtering-reddit-links-with-azure-cognitive-services-sentiment-analysis
title: "Filtering Reddit Links with Azure Cognitive Services Sentiment Analysis"
summary: "Building a web application to only show positive or negative stories from a subreddit."
image: 'filtering-reddit-links-with-azure-cognitive-services-sentiment-analysis\lead.png' 
tags:
- CognitiveServices
- F#
---

One of the fascinating capabilities of Azure Cognitive Services is the ability to get a sentiment score for a text string. The score is a numeric value between 0 and 1. Values closer to 1 indicate that the statement is conveying a positive sentiment. Values closer to 0 indicate a negative sentiment. 

This could be used to gauge how people feel about a product launch by getting the sentiment score of tweets that mention the product. On a recent [.Net Rocks episode, Phil Haack](https://www.dotnetrocks.com/?show=1553) talked about the potential to use sentiment analysis to monitor how GitHub contributors were feeling by analyzing the sentiment of their pull requests or their issues.

I thought it would be an interesting experiment to see if I could filter posts in a subreddit down to the posts that contain either a positive or negative sentiment. For example, could I get a view of the /r/programming subreddit that only contained posts with a positive sentiment? If so, it could be used to see what a particular subreddit is excited about. Conversely, it could also be used to filter a subreddit down to the negative posts. 

## The Technology Stack ##

In the past I've blogged about a library I built called [Fognitive Services](http://humbletoolsmith.com/2018/03/22/F-and-Cognitive-Services/), that wraps the Cognitive Services API calls in F# functions. I've found that useful in the past and I decided to that [NuGet package](https://www.nuget.org/packages/FognitiveServices.Text/) here. 


[![](/img/posts/filtering-reddit-links-with-azure-cognitive-services-sentiment-analysis/body.jpg)](/img/posts/filtering-reddit-links-with-azure-cognitive-services-sentiment-analysis/body.jpg)


Next, I had to figure out how to get data for a given subreddit. Reddit has a very nice and well-documented REST API. If possible, I wanted to consume that data with the [FSharp JSON Type Provider.](http://fsharp.github.io/FSharp.Data/library/JsonProvider.html) As a bonus, the [latest beta versions](https://www.nuget.org/packages/FSharp.Data/3.0.0-beta3) of the package support .Net Core. So I would have a chance to test drive that new functionality. 

To serve up the data, I decided to create an ASP.Net MVC Core 2.1 web application. The 2.1 version was released in the last few weeks and I wanted to try it out as well. Since of the focus of the first version of this app was connecting Reddit to Cognitive Services, I didn't spend a lot of time making the UI look polished. I decided to simply generate the UI with Razor right in the web app.

## Building the Back End with F# ##

F# Type Providers are almost magic. They are one of the best features of the language. Type Providers are plugins to the compiler itself that can generate strongly typed structures based on a data source. In this case, I want to generate code to consume the Reddit API.

<script src="https://gist.github.com/pottereric/dabe429063e914a9ba576fd650063989.js"></script>


The magic happens on line 4. I manually called the Reddit API and generated a file that contains the JSON response. The type provider is using that sample data to generate types for the Reddit API. After that single type definition statement, the RedditProvider type can now return strongly typed information from the Reddit API, complete with full Intellisense.

I could point the Type Provider directly at the Reddit API. But the Type Provider runs at compile time and I didn't want my compile time to always include a REST request.

The file contains some additional functions I used to test out the Type Provider. But the code listed above is the entirety of what I needed to write to consume the Reddit API. The GetTitles function returns a list of stories for the given subreddit.

Before I could use Cognitive Services I had to create the resource in the Azure portal. I have some unused MSDN Azure credits that I am using for this experiment, but there is also a free trial that I could have used.

The next F# module takes the list of stories and transforms it into a list of inputs for Fognitive Services. Fognitive Services sends the inputs to Cognitive Services and returns a list of sentiments scores. I then use the List.zip3 function to combine the list of Reddit items, the list of inputs, and the list of sentiment scores back into a single list. Then I map the result into a list of RedditTitleSentiment so that the names are clearer. 

<script src="https://gist.github.com/pottereric/22985b5e1aa5b0708ab7ac4b8758e8be.js"></script>

Lines 5 and 6 are all that is required to get the sentiment score for each story. That is the magic of Azure Cognitive Services. It just a small amount of code you can have access to a very sophisticated machine learning algorithm. 

In under 50 lines of code, I had everything I needed to retrieve the list of stories in a subreddit and assign them a sentiment score. 

## Building the Web Application ##

The web application is built with ASP.NET MVC Core 2.1. I admit I wanted to build something with the latest and greatest version of the platform and it went very smoothly. My primary concern was that there would be an issue integrating the C# web application with the F# class library. But I didn't have any issues with that. The F# list type isn't the same as the C# generic list type. But LINQ will work with both, so it is simple enough to convert the F# list type and an IEnumberable. 

Using attribute routing, I added a few extra routes in the controller to make sure that the site would work with or without the subreddit name in the URL. I also choose to follow the Reddit pattern of putting "/r" in the subreddit URLS. This means that you can get directly to the CSharp subreddit by browsing to http://emotionalreddit.azurewebsites.net/r/csharp. 

## Hosting the Web Application ##

I created a new App Service in Azure to host the web application. I put it in the same resource group with the Cognitive Service. I was able to publish directly from Visual Studio, which was only noteworthy because there was both a C# web application and an F# class library.

## Results ##

With the app fully functional, I can now get a sense for how well Cognitive Services evaluates sentiment. It definitely produces the desired effect. Like almost anything with machine learning, it isn't perfect. From my observations, it seems to work better on longer chunks of text. Filtering stories in [/r/todayilearned](http://emotionalreddit.azurewebsites.net/r/todayilearned) which tend to have longer titles seems more effective than posts in [r/programming](https://www.reddit.com/r/programming/) which tend to have shorter titles. 

You can try out the site for yourself at [http://emotionalreddit.azurewebsites.net/](http://emotionalreddit.azurewebsites.net/). Just specify the subreddit you want to filter and the sentiment level you want to see. 

If you want to see the code, it is available on GitHub at [https://github.com/pottereric/EmotionalReddit](https://github.com/pottereric/EmotionalReddit). 






