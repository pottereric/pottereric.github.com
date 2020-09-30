---
comments: true
date: 2020-09-27 4:00:00
layout: post
slug: if-unit-tests-were-seinfeld-characters
title: "If Unit Tests were Seinfeld Characters"
summary: "You need more than one kind of unit test."
image: 'if-unit-tests-were-seinfeld-characters\lead.png' 
tags:
- Unit Tests
---

As software developers we spend a lot of time writing unit tests. We worry about writing enough tests to give us good code coverage. We obsess over which test framework and test runner to use. We ensure that our tests run quickly. We run our test suite after every change and before each check in.
 
But do we think about the different types of tests that we need write? Do we ever take the time to think about how our tests complement each other? If our test suites are going to provide maximum value, the tests need to fill different roles and complement each other. We need to be intentional about types of tests we write.
 
![](/img/posts/if-unit-tests-were-seinfeld-characters/seinfeld-cast-321x350.jpg)

Seinfeld is arguably the best TV show of all time.  If you are a fan of the show you love to laugh with Jerry, George, Kramer and Elaine. The writers truly created classic characters. But what took the show to the next level was the brilliance in how the separate characters’ storylines intersected and complemented each other. Let's look at the role of each Seinfeld character and how we should have unit tests that fulfill similar roles and complement each other in our unit testing just as well as Jerry, George, Kramer and Elaine did on Seinfeld.
 
## Jerry Tests ##
 
Jerry was the central character on Seinfeld. Episodes generally revolved around his life. It seemed things always worked out for Jerry. In the episode titled "The Opposite," Kramer nicknames Jerry 'Even Steven' because whenever something went wrong for him, something good happened to balance it out. 

![](/img/posts/if-unit-tests-were-seinfeld-characters/JerryA.jpg)

Throughout the series Jerry generally enjoyed a successful career and dated an endless stream of beautiful women. Nearly every episode included Jerry obsessing with some obscure fault he discovered in each woman. Even so, Jerry came across as the normal and stable one of the bunch. It is impossible to picture this group of friends without Jerry in it.
 
As software developers we need to have Jerry tests. We often call these happy path tests. These are the tests that validate that the software behaves as expected when everything goes right. These are the tests that cover the central functionality and the functionality that the software revolves around. We need tests as steady and neurotic as Jerry.

Let's say that you are writing an application for a client that manufactures widgets. Your application needs to collect data from the machines, aggregate the data about how many widgets are being manufactured per day per machine, and then store the results. Jerry tests would validate that when a normal amount of parts are being manufactured on a normal day, the results are correctly calculated and stored. The Jerry tests are vitally important because they cover the cases the software will encounter the majority of the time. But you do need other kinds of tests. 
 
Every central character with great hair like Jerry’s needs a mess of a sidekick, preferably one without hair.  George Castanza’s life and baldness supplied an endless list of problems and failures for Jerry to find to mock.
 
## George Tests ##
 
What didn’t go wrong for George?  His life was marked by epic failures. George found a way to screw up even the simplest of things. 

![](/img/posts/if-unit-tests-were-seinfeld-characters/Costanza.jpg)

George specialized in underachieving and working as little as possible.   His career included being declared dead by boss George Steinbrenner and posing as a latex salesman for the imaginary company, Vandelay Industries. 

George’s love life was a wreck as well.  He found a way to implode every good relationship that came his way. The epitome being when his fiancé Susan died from licking poisonous glue on the wedding invitations George picked out because they were cheap. He seemed to fail at every turn. 

Our tests suites need to have George tests to reveal failure cases in our software. Some George tests cover little things, like the user entering invalid data. Some George tests cover big things, like failures to find required files. For our software to be robust, it needs to be able to handle errors. If we are going to have confidence in our error handling code it needs to have George tests.

Going back to our example with the manufacturing application, George test would cover the case when one of the machines produces zero parts. Let's say that you have one class that handles the aggregation and several machine provider classes that handle the communication with the machines. George tests of the aggregation class would cover the cases where the machines providers return null or throw an exception.
 
George tests will cover common failure modes, but our software also needs to be able to handle the bizarre cases. On Seinfeld the character that encountered and generated the most bizarre situations was Kramer.
 
## Kramer Tests ##
 
Kramer was constantly involved in situations that were downright outlandish. How could anyone but Kramer get fired from a job he never had?  Or be accused of being a serial killer and not know it?  How did he end up driving a ladder truck through New York City?
 
![](/img/posts/if-unit-tests-were-seinfeld-characters/KramerDreamcoat.jpg)

His friends are constantly bewildered by his bizarre lifestyle. In one episode Kramer found the Merv Griffen set and assembled it in his apartment and lived as if he were on a talk show. In another episode Kramer somehow got mistaken for a pimp while wearing a costume from Joseph And The Amazing Technicolor Dreamcoat. 
His unexpected antics often screw up his friends’ plans. People never know what to expect with Kramer. He bizarre, unreliable and unpredictable.
 
When we’re testing our software we are going to need Kramer tests to cover rare cases. These are edge cases. Bizarre cases. The things that one user in a million will try. If our software is going to have a large user base eventually it will encounter the issues that only happen once in a blue moon. Kramer tests give us confidence that blue moons won't crash our software.

In our example application, Kramer test would test parts per day rates for days that have 23 or 25 hours. (Thanks daylight savings time.) Kramer tests would also cover cases where an abnormally large number of parts are made, possibly enough to overflow an integer. 
 
Not all rare cases are bizarre. Some are just complicated, and our software needs to be able to handle those situations. On Seinfeld, the character who always seemed to end up in overly complicated situations was Elaine.

## Elaine Tests ##
 
Every aspect of Elaine’s life is unnecessarily complicated. Most of her issues revolve around situations in her job or her love life. Her dilemmas are usually a perfect storm of events caused by her and her friends’ impulsive decisions.

![](/img/posts/if-unit-tests-were-seinfeld-characters/ElaineJFKGolfClubsjpg.jpg)

In the episode “Bottle Deposit” Elaine overbids on JFK’s golf clubs for her boss to beat her bra-less rival Sue Ellen Mischke. Then the clubs are stolen when a rogue mechanic takes off with Jerry’s car because Jerry doesn’t want to pay to fix it.  Elaine’s only hope then rests on Kramer who is tailing the car through Ohio while driving a mail truck full of cans to recycle in Michigan.  Who else, but Elaine could get herself into such a complicated situation?

Elaine tests cover situations were two or three things have to happen together in order for the test case to fail under test. Often, these tests are the ones that require mocks or stubs in order to isolate the code being tested. 
 
In the manufacturing application, Elaine tests would cover situations where multiple instances of the application are running at the same time, potentially generating a race condition. They might also cover cases where the communication with the machines is very slow because of a huge amount of traffic on your network.

Elaine tests can take time to write, especially when you need to generate large datasets or populate complex classes. The result is worth the extra effort though. You can make the work easier by utilizing a mocking framework or implementing the mother or builder pattern to generate your test data. An additional benefit to any of these techniques is that you can reuse these tools in other Elaine tests.
 
## Every Show Needs Extras ##
These four types of tests are the main types of tests that you will need. In the same way that Seinfeld needed an array of characters to round out each episode, you will need other types of tests. Which types you need will depend on your application.
 
Do you remember the episode where Japanese tourists misunderstood he conversion from Yen to dollars and ended up sleeping in Kramer's over-sized dresser? Well, don’t forget you may need tests to cover currency exchange rates. 

Who can forget the episode where Elaine's boyfriend Puddy is an ice hockey psycho fan who wears face paint and scares a poor priest? Remember, you may need tests to cover what data will get visualized.

Puddy and Elaine's relationship was funny in it's own right for how many times they broke up and go back together.

    do {
    	Eliane.Dump(Puddy)
    	Elaine.GetBackTogetherWith(Puddy)
    } while (season == 9 && (episode == 1 || episode == 2)

Do you need to have a test that will test your software's behavior if one section of code gets called repeatedly in quick succession?

Another unforgettable was the Soup Nazi. This guy would refuse to serve customers in his restaurant for trivial reasons with his classic catch phrase "No soup for you!" Do you have tests that cover situations where your database connection is denied?

If you only had one kind of test you wouldn't truly be exercising the system. You need all kinds of tests to give you confidence that the system will work as expected in all kinds of situations. Remember, the fundamental reason we write unit tests is to have confidence in the software.  If you don't have a full cast of tests, you probably have bugs you won't know about until later.
> Serenity now, Insanity later. - Lloyd Braun
 
## Ensemble Cast ##
A show based on only one of these classic characters from Seinfeld would not be fun to watch for very long.  It is in how they related to each other and how their storylines intersected that keeps us watching. 

Some of the best moments in the show happened as multiple elements of the characters’ storylines came together. 

In “The Marine Biologist” episode, the final scene is amazing because it brings together the story about George pretending to be a Marine biologist to impress his date and Kramer hitting golf balls into the ocean. 

“The Apology” episode had a beautiful moment when Kramer’s obsession with staying in the shower as long as possible intersects with Elaine and Jerry’s germaphobe plotline. 
Happy Ending  

Our unit test suites should have this same type of fusion. There should be a set of tests that cover the happy path and a group of tests that cover failure cases. There should also be tests that cover bizarre situations as well as the complicated situations that could occur. In addition, there should be other tests that cover the problem areas specific to your application and your domain. If you have a full cast of tests, hitting 'Run All' in your test runner will lead to a happy ending to your development story.

 
 
