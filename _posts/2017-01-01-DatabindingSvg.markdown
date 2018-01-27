---
comments: true
date: 2017-01-01 14:30:00
layout: post
slug: Databinding SVG with Aurelia
title: Databinding SVG with Aurelia
summary: 'Using Aurelia to bind a visual element to a view model'
image: 'Databinding-SVG\main.png'
tags:
- Aurelia
- Design Patterns
---

Recently my son was looking at a globe and asking me questions like 'Is Ecuador bigger than Texas?' I found the answer quickly on Wikipedia, but it got me thinking that it may be fun to have a graphical representation of the comparison. 

I decided to put the GUI together as a web application using Aurelia. I wanted to have a list of checkboxes to allow my son to select the countries or states that he wanted to compare. When geographic regions were selected, circles would be drawn that were proportional to the square miles in the region. 

My first thought was to have a delegate on each checkbox that would draw the circles programmatically. That certainly would have worked, but then I stumbled upon [this Stack Overflow answer](http://stackoverflow.com/a/29515017/26339) from @AshleyMGrant. 

It helped me realize that because SVG elements are regular HTML elements, you can bind to them with Aurelia just like you would bind to any other elements. All I had to do was use the repeat.for binding on a circle element. Each circle is bound to a geographic region in the view model, the same elements that were bound to the check boxes. Each geographic region in the view model has a number of square miles associated, and the radius of the circle is bound to this value. 

<script src="https://gist.github.com/pottereric/105e5e6cf0073a39818d8efad6976b90.js"></script>

One of the things that I like about this solution is that it takes advantage of the Model View Presenter/Controller pattern. The model contains all of the relevant data. It doesn't concern itself with how it is displayed. The view has two different representations of the data, one as a list of checkboxes, one as graphical objects. 