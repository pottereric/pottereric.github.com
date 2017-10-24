---
comments: true
date: 2017-10-24 4:30:00
layout: post
slug: cosmosdb-and-flow
title: Test Drive => Cosmos DB with Microsoft Flow
summary: 'Combining Microsoft Flow and CosmosDB is fast and easy.'
image: 'CosmosDB-And-Flow\lead.png'
tags:
- Flow
- CosmosDB
---

Microsoft recently a preview version of their Microsoft Flow connector for CosmosDB. If you haven't tried out Flow before, connectors are the tools that allow you to integrate external services into your workflows. Connectors allow you to read or write from data sources like Twitter, Office 365, Dropbox and much more. 

Flow already had connectors for SQL Server, PostgreSQL, and MySQL. They work great for situations where you want relational data. But I find that especially when I am working with disparate systems in Flow, it is much easier to store data in a less structured way. This makes working with CosmosDB and it's document store a very natural fit. 

// TODO

[![](/img/posts/CosmosDB-And-Flow/ConfiguringTheCosmosDBConnector.png)](/img/posts/CosmosDB-And-Flow/ConfiguringTheCosmosDBConnector.png)

The only hitch I ran into while building a workflow was that the Flow engine didn't require me to have an "id" field in my JSON document. The first time I ran the Flow, Cosmos returned an error because there was no "id". Once I added it, my flow worked correctly. Becuase I was storing tweets, using the tweet id and the document id was a natural fit.

Summary:
* CosmosDB is a great way to persist data from Microsoft Flow
* Make sure your JSON documents have an "id" field before storing them.

