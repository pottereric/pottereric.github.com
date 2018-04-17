---
comments: true
date: 2018-04-08 4:00:00
layout: post
slug: analyzing-the-stirtrek-conference-sessions-with-azure-cognitive-services
title: "Analyzing the StirTrek conference sessions with Azure Cognitive Services"
summary: "What can we learn from looking the 2017 and 2018 StirTrek session data?"
image: 'analyzing-the-stirtrek-conference-sessions-with-azure-cognitive-services\lead.png' 
tags:
- CognitiveServices
- F#
- Canopy
---

In a [previous post](http://humbletoolsmith.com/2018/03/22/F-and-Cognitive-Services/), I looked at how I could use Azure Congitive Services to look at the keywords from the [StirTrek](https://stirtrek.com/) conference session titles. In this post I want to continue that exploration and see what we can learn about the service and the conference.

I am going to use the Text Analysis API. Specifically I am going to call the API that will return the key phrase or phrases for any input text. For example, if you pass it "[Boom! From Combat Engineer to Software Engineer](https://stirtrek.com/sessions/session/106)" (which is a real session at StirTrek this year), it will return "Combat Engineer" and "Software Engineer". 

The API could also detect which language the given text was in. But since all of the StirTrek sessions are in English, it would be very interesting in this experiment. There is also an API that returns a score representing the sentiment of the input text. I plan to explore that in a future blog post.

## Experiment 1: Repeated Phrases in Titles

For the first part of the experiment, I wanted to see which key phrases appear in session titles both this year and last year. The StirTrek web site lists information for both years, so I can collect it with Canopy rather easily. As I demonstrated in the previous post, I used the [Fognitive Services](http://humbletoolsmith.com/2018/03/22/F-and-Cognitive-Services/) library to pipe the titles into Azure Cognitive Services. I used the Set operations in F# to create sets from the 2017 and 2018 title key phrases and then created a union of the results, giving the key phrases that appeared both years.

Using this method, I found that the key phrases that were repeated were 'machine learning' and 'sql server execution plans'. One thing I noticed right away was that certain technologies were missing from the list. For example, 'Angular', 'React', and 'UX' appear in session titles both years. So Cognitive Services either has a hard time recognizing technology names or it didn't see them as the key phrases in their respective sentences. The fact that the technologies don't show up in the results means that we can learn something about the conference beyond what technologies are popular at the time. 

The fact that machine learning showed up both years is fascinating to me, especially since Cognitive Services is an nice abstraction layer over very sophisticated machine learning algorithms. For what it is worth, here are the machine learning sessions from both years:
- Machine Learning in R (2018)
- Using EEG and Machine Learning to Perform Lie Detection (2017)

## Experiment 2: Most Common Phrases in Session Details

For the second experiment, I wanted to look at the abstracts. We can still retrieve them with Canopy. But because there is so much more text in the abstracts, it isn't helpful to look at which phrases appear in both years. There would be too many results. So instead I will append the key phrase lists together and count how many total times the phrase appears. So can see the raw results [here](/content/StirTrekSessionKeywords.txt). I think it shows something interesting about the conference.

The top two results (_session_, _talk_) are meta information about the conference, so that isn't that interesting. The next highest results is _code_, appearing 13 times. This is also uninteresting as it restates the fact that this is a developer conference. The same of true of _developers_ appearing 9 times. The phrase _way_ appears 10 times and _ways_ appears 7 times. This would seam to indicate the the conference has an emphasis on showing how things can be done.

The first surprising result is that _time_ shows up 9 times. There is clearly an emphasis on the fact that time is important to developers. The word _tools_ appears 8 times, indicating that the conference wants to teach developers about the tools that can help them and presumably help them save time.

The result in the top 10 that surprised me the most was _people_, appearing 7 times. The related terms _customers_ and _teams_ both appear 4 times. Clearly the conference organizers recognize that some of the biggest challenges that we face as developers are not technical at all, but instead have to do with interacting with our fellow humans. 

## Next Steps

I was impressed with how easy it was to get generate the results sets. It would be interesting to look at the some information but for a conference where I could get the results for multiple years. It would also be interesting to compare results between to conferences. I'll try and track that down for a future blog post.

Do you have an idea for something I should try to abstract from a conference data set with Cognitive Services? Leave a comment below with any suggestions. Or just find me on Twitter and let me know what I should be looking for.


