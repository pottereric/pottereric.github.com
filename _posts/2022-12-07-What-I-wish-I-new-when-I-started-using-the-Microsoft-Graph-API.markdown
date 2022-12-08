---
comments: true
date: 2022-12-07 4:00:00
layout: post
slug: what-i-wish-i-new-when-i-started-using-the-microsoft-graph-api
title: "What I wish I new when I started using the Microsoft Graph API"
summary: "Tips to get started faster building your first app with Microsoft Graph."
image: 'what-i-wish-i-new-when-i-started-using-the-microsoft-graph-api\lead.png' 
tags:
- CSharp
---

Note: This post is a part of the 2022 C# Advent Calendar. You can see the rest of the posts [here](https://csadvent.christmas/).

The Microsoft Graph API is a powerful way to automate interactions with the Microsoft apps you use every day. For example, you could use it to generate Todo items in your Microsoft TOOD account based on data in an Excel spreadsheet. Or you could respond to an event in your custom application by automatically scheduling an Outlook meeting. You can do all this and more from a single API. Or, if you're a C# developer, you can do it with a single [NuGet package](https://www.nuget.org/packages/Microsoft.Graph/). (packages are also available for other languages)

I like to think of working with the Graph API as being a two step process:
1. Authenticate
2. Manipulate

In order to get started working with the Graph API, you have to choose how you are going to authenticate your application and your user. I'm not going to cover authentication in this blog post because it varies so much based on your context and the kind of application you are building. I recommend looking at the [official docs](https://learn.microsoft.com/en-us/graph/sdks/choose-authentication-providers?tabs=CS) to select your authentication provider. More details about how to configure authentication are available in [other posts](https://davidgiard.com/using-the-ms-graph-api).

## Abstract away the authentication details by passing around a GraphServiceClient instance ##
For the applications I've built, I have a class that builds and returns an instance of GraphServiceClient. This means that my authentication provider logic can be encapsulated in that class. The rest of the application interacts with Microsoft Graph via the GraphServiceClient instance. 

## Explore the Graph API with the Graph Explorer ##
Microsoft provides a powerful tool called the [Graph Explorer](https://www.nuget.org/packages/Microsoft.Graph/) to experiment with the available APIs. It can work with dummy data. It can also work with your real data if you authenticate it. The Graph API is expansive. It covers everything from Excel, to Outlook, to OneDrive, and more. Using the Graph Explorer will give you an idea of what is possible. 

## Checkout the GraphServiceClient.Me Property ##
If the authentication method you chose authenticates a user and not an application, you can get a lot of valuable information from the Me property of the GraphServiceClient object. For example, you can get the user's calendar or their ToDo list from properties of this property. 

## Collections are Paged ##
Because the lists that are returned could be very long, all collections are paged. If you want to query all of the items in your Outlook calendar, it could be hundreds or thousands of items. When you query the collection, you will only get the first page. You can use the NextPageRequest property of the collection to get the next page. 

## Summary ##
This is far from an exhaustive explanation of how to get started with the Graph API. But hopefully, this information will get you started a little faster. 

The Graph API enables you to build tools to make your work easier. Have fun exploring all of the possibilities. 

Stay Curious. 