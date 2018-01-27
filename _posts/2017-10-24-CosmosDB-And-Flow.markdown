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

Microsoft recently a preview version of their Microsoft Flow connector for CosmosDB. If you haven't tried out Flow before, connectors are the tools that allow you to integrate external services into your workflows. Connectors allow you to read or write from data sources like Twitter, Office 365, Dropbox and many more. 

Flow already had connectors for SQL Server, PostgreSQL, and MySQL. They work great for situations where you want relational data. But I find that especially when I am working with disparate systems in Flow, it is much easier to store data in a less structured way. This makes working with CosmosDB and it's document store a very natural fit. 

To do the CosmosDB integration, I opened up a Flow. I already had a flow that would pick certain tweets off of my timeline, so I just edited that flow. I clicked on the "Add an action" button. From the dialog, I searched for "CosmosDB" and in this case, I picked "Azure Cosmos DB - Create or update document". But as you can see, there are many other CosmosDB actions I could have taken.

[![](/img/posts/CosmosDB-And-Flow/ChoosingACosmosDBAction.png)](/img/posts/CosmosDB-And-Flow/ChoosingACosmosDBAction.png)

Because it was the first time I had connected to CosmosDB, I was prompted for connection information about my Cosmos database. I had already created one inside the Azure Portal, so I just had to enter the information. Otherwise, I would have needed to create the database. The last thing I had to do was fill in the JSON that I wanted to insert. The Flow editor allows you to click on the data fields that you want to include. So in my case, I was able to include fields from my twitter input right in the JSON.

[![](/img/posts/CosmosDB-And-Flow/ConfiguringTheCosmosDBConnector.png)](/img/posts/CosmosDB-And-Flow/ConfiguringTheCosmosDBConnector.png)

The only hitch I ran into while building the workflow was that the Flow engine didn't require me to have an "id" field in my JSON document. The first time I ran the Flow, Cosmos returned an error because there was no "id". Once I added it, my flow worked correctly. Becuase I was storing tweets, using the tweet id and the document id was a natural fit.  I also had a small issue at first because I pasted in some JSON and the JSON editor didn't think it was valid. Once I removed the unnecessary whitespace in the JSON everything was fine. Since this is still a preview version of the CosmosDB connector, I'm sure these little issues will be resolved before the final release. 

Summary:
* CosmosDB is a great way to persist data from Microsoft Flow
* Make sure your JSON documents have an "id" field before storing them.

