---
comments: true
date: 2016-08-19 14:30:00
layout: post
slug: Validating-List-Sorting-with-Canopy
title: Validating List Sorting with Canopy
summary: 'Validating List Sorting with Canopy'
image: 'Validating-List-Sorting-with-Canopy\canopylink.jpg'
tags:
- Canopy
- FSharp
---

One of the things that F# is particularly good at is dealing with things as lists. So when I had a Canopy test that needed to verify the elements on a page were sorted correctly, I looked for a way to leverage F#'s strengths. I am primarily a C# developer, so my first instinct was to get the elements, loop through them and check the ordering. But after some digging I came up with this solution. 

<script src="https://gist.github.com/pottereric/23d50892fecc12356a03d98c2378bb7a.js"></script>

There is a lot going on in a short chunk of good. Line 6 defines the canopy test. Line 7 calls a function I have defined elsewhere to log in the administrator user. Line 8 uses canopy's ability to use CSS selectors to retrieve the elements in the rightmost column of a table. This returns a list of IWebElements. Line 9 uses the F# pipe forward operator to pass the result of line 8 into a method that gets the text of each element. The resulting list is passed to the isSorted function. 

The isSorted method uses some of F#'s sophisticated list operations. The Seq namespace contains F#'s methods that operate on [sequences](https://docs.microsoft.com/en-us/dotnet/articles/fsharp/language-reference/sequences). The pairwise function takes a list and returns a list of all of the pairs in the list. For example:

a,b,c,d,e becomes (a,b),(b,c),(c,d),(d,e)

The forall method takes a function and returns true if the the function is true for all of the items in the list. In this case, the list is the list of pairs returned from pairwise. 

The result of isSorted is passed to Canopy's is method on line 11. The is method determines if the test passes or fails. 

Thanks to @ReidNEvans who helped me clean up this code. He also pointed out that I could have used the Fold function to validate the sort. Which I may explore in a future blog post. 

One of the things I love about Canopy is that you don't need to know much about F# to be productive with Canopy. But if you do know F#, you have it's full power at your finger tips. 
