---
comments: true
date: 2017-12-30 14:30:00
layout: post
slug: testing-out-the-azure-serverless-tools
title: Test Drive- Serverless Web Applications
summary: 'Taking the Azure serverless tools for a spin'
image: 'Testdrive-Serverless\lead.png'
tags:
- Flow
- CosmosDB
- AzureFunctions
---

The last time I was in the market to buy a car, I started by reading a lot of reviews. I talked to people that already owned the cars that I was interested in. I did comparisons of my top choices online. But before I would ever buy a car, I took it for a test drive. In fact I took several cars for test drives before buying the one that I liked the best.
 
I often take a similar approach with technology. I frequently listen to podcasts or check sites like Hacker News just to know what the trends are. I follow a large number of people I respect on Twitter so I can know what new tech they are excited about. At conferences, I'll start up random conversations with people in the hall or in line for meals in order to know what they are interested in. When a technology seems interesting enough, I'll start to read up on it, reading some reviews, overviews and blog posts (just like you are right now). But before I would ever use some new technology on a production software product, I take it for a sort of test drive.

The technology trend that is getting hard to ignore this year is serverless web applications. You can argue that the name "serverless" is misleading, but I'll use it because that seems to be what people are calling it. In serverless applications, the server is obviously there. But the technology tries to abstract it away from the developer's concern. Because I've done much of my work on the Microsoft stack, I decided to try out the Azure serverless offerings. 

## The Application ##

For it to be a proper test drive, I wanted to come up with a nontrivial application. I decided to build something that would monitor my twitter feed for URLs that were tweeted by multiple people. So these were the requirements that I came up with:
1. Monitor my Twitter feed for tweets containing URLs, and store the tweets that are found.
2. Expand shortened URLs to the target URL.
3. Query the collection of full URLs for links that appear multiple times.
4. Display the results on a web page.

It isn't the worlds greatest application. But then again, no test drive is the world's greatest road trip. I figured that there was enough in these requirements to get a good feel for how these new technologies worked in real world scenarios.

## The Architecture ##

In order to monitor my Twitter feed, I used Microsoft Flow. It has a WYSIWYG editor that makes it dead simple to create simple workflows. It has adapters for Twitter as well as for CosmosDB, which is what I chose for my storage needs. CosmosDB is the new NoSQL offering in Azure. It works particularly well in serverless applications, so I wanted to kick it's tires. I also wanted to try out the ability to write stored procedures in JavaScript. So I did part of the querying in a stored procedure.

I wanted to try out Azure Functions to handle the business logic. I use a timer to kick off a function that expands the URLs. I use another function to aggregate the data and serve it up as a REST API. That API is consumed by an HTML page that has no server-side rendering. There is an Azure Web App that hosts the HTML, but the page only uses Axios to call the REST API and Vue to display the data.

Here is the whiteboard diagram of the system.

[![](/img/posts/Testdrive-Serverless/Architecture.jpg)](/img/posts/Testdrive-Serverless/Architecture.jpg)

## The Result ##

In the end, I web page I can load that will display the desired results. It isn't the next Uber of anything. But it does meet the requirements and it does qualify as 'serverless'. Here are my opinions of the technologies that I tried.

I detailed my thoughts on Microsoft Flow in a [previous blog post](http://humbletoolsmith.com/2017/10/24/cosmosdb-and-flow/). The quick recap is that it was delightful to work with. The UI was intuitive. I got the functionality that I wanted very quickly. 

I really enjoyed working with Azure Functions. I'll have a longer blog post later with more details. But here I will just say that they functioned the way that I expected and I was able to focus on my logic, not on the hosting aspects. So it succeeded in abstracting away the server concerns.

CosmosDB was fascinating. Of the things I tried in this project, it had the steepest learning curve. But it may also have the biggest benefits. I'll also put a much longer review in a future blog post. For the time being, I'll simply say that CosmosDB has a bright future. But right now it is a still a very young project, which leads to pain points at times.

The web page was so trivial that I would consider it a proper test drive. But I was impressed how quickly I was able to put something together with Vue and Axios. For bonus points, I wrote the web page on an Ubuntu machine using only Vim. I deployed it to Azure with Git. But even with these arbitrary constraints, the whole development process was quick and easy.

While the whole system isn't getting used heavily, I've been impressed with how little it is costing me. The timers run parts of the system every day. I have been loading the web page almost every day. The whole thing is costing me less than $60 a month, which is easily within my $150 monthly allowance with my MSDN subscription. 

Overall, I was very impressed with how well the various peices fit together. The integration between Flow and CosmosDB worked great, especially considering it is still preview functionality. The integration between CosmosDB and the Azure Functions was also very good.

## Conclusion ##

I can see why there is so much hype around serverless applications. It was nice to be able to write my business logic and ~~never~~ rarely think about the web server. Having completed the test drive, I have already recommended Azure Functions for use in an upcoming project at Aptera. CosmosDB has a ton of promise. I'm sure I'll use it professionally in the future as well. Microsoft Flow was great for my personal project. On a bigger project I would probably recommend Logic Apps. 

It was a great learning experience building with these new technologies and I look forward to working with them in the future.
