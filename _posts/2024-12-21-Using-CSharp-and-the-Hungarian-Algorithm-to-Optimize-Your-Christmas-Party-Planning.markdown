---
comments: true
date: 2024-12-21 4:00:00
layout: post
slug: using-csharp-and-the-hungarian-algorithm-to-optimize-your-christmas-party-planning
title: "Using C# and the Hungarian Algorithm to Optimize Your Christmas Party Planning"
summary: "Use an algorithm to assign the best cook to each food."
image: 'using-csharp-and-the-hungarian-algorithm-to-optimize-your-christmas-party-planning\lead.png' 
tags:
- C#
---

This post is part of [C# Advent](https://csadvent.christmas/) organized by @mgroves.

This is the time of the year when many of us are planning Christmas Parties. There is often a sign-up where attendees can indicate what food they want to bring. These usually ensure people bring the right mix of cookies, pie, and candy canes. But it doesn't ensure the optimal assignments. 

The problem is that these sign-up sheets work on a first-come, first-served basis. For example, maybe Mark was the first one to open the sign-up, and he signed up for pie. When Janet opened the sign-up form, she couldn't sign up for pie because Mark had already done so. This is a problem because everyone knows that Janet makes the best pie. Seriously, how does she make the pie crust that delicious? Mark makes cookies that are just as good as his pie. So we all want Janet to bring the pie and Mark to bring the cookies. 

What we want is a way for everyone to indicate what items they want to bring and assign a score for each item indicating how much they want to bring that item. Then, we can run an algorithm to determine the optimal assignments for who should provide which item. 

[Assignment algorithms](https://en.wikipedia.org/wiki/Assignment_problem) are a surprisingly well-studied topic in computer science. There are algorithms for many different variations for different scenarios.  Sometimes, you want to make assignments where both sets have preferences in their pairing. But in our case, only one set has a preference. Janet has a strong preference that she bring the pie. But the pie doesn't care who bakes it. Although if the pie were sentient, it would absolutely want Janet to bake it. But if the pie were sentient, we'd have moral questions about eating it. Forget I ever mentioned the pie. The pie doesn't have a preference for the assignment, so we need a one-sided assignment algorithm. 

What we want is an implementation of the [Hungarian Algorithm](https://en.wikipedia.org/wiki/Hungarian_algorithm). Fortunately, there is a good open source implementation of the [Hungarian Algorithm available on Nuget](https://www.nuget.org/packages/HungarianAlgorithm) thanks to a user, Vivet. 

### Modeling the choices
The Hungarian optimizes for an overall "cost." Each potential pairing is assigned a cost where a lower value means that it is a better choice for the solution than a higher value. 

In our example, we want the "cost" of Janet bringing a pie to be low because Janet makes the best pie. As mentioned before, Mark's cookies and pie are equal, so they get the same "cost."

<table>
<thead>
	<tr>
		<th>Cook</th>
		<th>Cookies</th>
		<th>PIE</th>
		<th>Candy Canes</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>Mark</td>
		<td>3</td>
		<td>3</td>
		<td>5</td>
	</tr>
	<tr>
		<td>Janet</td>
		<td>3</td>
		<td>1</td>
		<td>7</td>
	</tr>
	<tr>
		<td>Bob</td>
		<td>4</td>
		<td>5</td>
		<td>5</td>
	</tr>
</tbody>
</table>



### Using the Hungarian Algorithm with C#

The input is a two-dimensional array that represents the choices. The array doesn't have any of the label data, just a matrix of the costs. Pass the array to the FindAssignments method. 

{% raw %}
int[,] costs = {{3, 3, 5}, 
                {3, 1, 7},
                {4, 5, 5}};
                
int[] result = HungarianAlgorithm.FindAssignments(costs);
{% endraw %}


The result is an array that indicates the optimal pairings. The trickiest part of this whole process is that the data that is returned is a collection of indexes, not the names of the pairs. The input data wasn't labeled, thus the output values aren't labeled either. You will have to track them separately. 

In our case, the output would be [0,1,2]. 

<table>
<thead>
	<tr>
		<th>Index</th>
		<th>Value</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>0 - Mark</td>
		<td>0 - Cookies</td>
	</tr>
	<tr>
		<td>1 - Janet</td>
		<td>1- Pie</td>
	</tr>
	<tr>
		<td>2 - Bob</td>
		<td>2 - Candy Canes</td>
	</tr>
</tbody>
</table>

