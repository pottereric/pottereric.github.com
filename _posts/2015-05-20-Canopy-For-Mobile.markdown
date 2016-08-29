---
comments: true
date: 2015-06-25 14:30:00
layout: post
slug: Using Canopy To Test Responsive Design
title: Using Canopy To Test Responsive Design
summary: 'Using Canopy To Test Responsive Design'
image: 'Canopy-For-Mobile\canopylink.jpg'
tags:
- Canopy
- 
---

I love [Canopy](http://lefthandedgoat.github.io/canopy/index.html) for writing integration tests for web applications. One of Canopy's best kept secrets is resize. It allows you to resizing the browser to represent different screen sizes. For example, the layout for my blog has some responsive elements. If the browser is as narrow as it is on a phone, the search box at the top will go away and the home link will be moved from the top bar into a menu. That menu has a button that will only be displayed on smaller screens.

Lets say I want to write two Canopy tests to make sure the button is hidden when the page is viewed on a laptop and it is displayed when the page is viewed on a phone. You could use the following code.

    
    "The navbar button is hidden for a laptop screen" &&& fun _ ->
    	resize (1024,768)
    	notDisplayed "div.container a.btn.btn-navbar"
    
    "The navbar button is displayed for a phone screen" &&& fun _ ->
    	resize screenSizes.iPhone5
    	displayed "div.container a.btn.btn-navbar"


In the first test, I call the resize method passing a tuple representing the minimum laptop screen that I want to test. This will resize the browser before executing the assertion on the next line.

In the second test, I make use of one of the constants that are defined by Canopy to automatically resize the browser to a know phone screen size.

Running these two test will give me confidence that the page is responding to various screen sizes. It is that easy and it can be very useful.
