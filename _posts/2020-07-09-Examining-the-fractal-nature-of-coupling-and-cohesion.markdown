---
comments: true
date: 2020-07-09 4:00:00
layout: post
slug: examining-the-fractal-nature-of-coupling-and-cohesion
title: "Examining the fractal nature of coupling and cohesion"
summary: "Code coupling can happen at different levels of magnification. Visualization tools can help you detect it."
image: 'examining-the-fractal-nature-of-coupling-and-cohesion\lead.png' 
tags:
- Object Oriented Design
- NDepend
---

One of the beautiful things about software development is that you can build any application you want, no matter how large or small, with code. As Fred Brooks so elegantly said
"The programmer, like the poet, works only slightly removed from pure thought-stuff. He builds his castles in the air, from air, creating by exertion of the imagination."
We write code to build functions. With more code, we compose the functions into objects or modules, creating a higher level of abstraction. With even more code, we create more levels of abstraction by creating packages or assemblies. 

I've always been fascinated by the fact that some attributes of the code apply equally at each level of abstraction. In particular, the concepts of coupling and cohesion apply at the function level, the class level, and at the package level.

Coupling is the degree to which a unit of code is dependant on other units of code. Ideally, code has few dependencies. This makes it easier to understand, modify, and fix. In order for the software to do anything meaningful, the separate code units must work together. So our goal is not to eliminate coupling, but to minimize it. Functions can be coupled, modules can be coupled, and packages can be coupled.

If we know that we want to minimize coupling, how do we analyze our code to blocks that might be problematic? We can look at the code itself to find coupling, but it is easier to find it using a visualization tool. Fortunately, C# developers have some good options for tools.

Visual Studio ships with a tool called Code Map that provides a graphical way to look at the dependencies between classes. But the [NDepend](https://www.ndepend.com/) extension provides an even better way to visualize dependencies with its Dependency Graph tool.

As an example, let's look at the code for the open-source tool called FancyZones that is a member of the [Microsoft PowerToys](https://github.com/microsoft/PowerToys) project. It is a WPF project that enables users to define zones on their screen where they can snap windows. 

In this brief video, you can see what the graph looks like as you zoom in and out on the code.

<iframe width="560" height="315" src="https://www.youtube.com/embed/SzaChMmFTuo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

If we look at the graph while zoomed to the level of the namespaces, we can see the coupling between the them.

![Namespace Level Dependencies](/img/posts/examining-the-fractal-nature-of-coupling-and-cohesion/Namespace Dependencies.png)

The arrows represent dependencies. In the example above, you can see that FancyZonesEditor.Converters has a dependency on FancyZonesEditor, which in turn has dependencies on FancyZonesEditor.Utils and FancyZonesEditor.Models. The dependency graph also colors objects based on their relationship to the selected object. In the image above, FancyZonesEditor is red because it is selected. FancyZonesEditor.Converters is green because it is a caller of FancyZonesEditor. FancyZonesEditor.Utils is green because it is a callee. And FancyZonesEditor.Models is pink because has a mutual dependency with FancyZonesEditor.

At this level of magnification we can start to see how the high level structures in this code based are related to one another and how they are coupled. If we zoom in, we can get the same information for the classes.

![Class Level Dependencies](/img/posts/examining-the-fractal-nature-of-coupling-and-cohesion/Class Level Dependencies.png)

Now we are looking at all of the classes in the FancyZonesEditor namespace. Notice how the dependency arrows have different widths. NDepend draws the widths proportional to the number of dependent items. You can quickly see that GridEditor has a stronger coupling with GridZone and weak coupling with App. You can use this information to quickly analyze the design of your classes. If there is a dependency that is stronger than it should be, it will be obvious in this view and you can begin to refactor it.

Let's zoom in further and examine the functions inside of the GridEditor class.

![Function Level Dependencies](/img/posts/examining-the-fractal-nature-of-coupling-and-cohesion/Function Level Dependencies.png)

Just like at the other zoom levels we see blocks of code and the dependencies between them. Again we see callers in green and callees in blue. 

The thing that is fascinating is how all three images look generally similar. In the same way that the Mandelbrot set or a Jackson Pollock look generally similar at different levels of magnification. 

This illustrates the importance of minimizing coupling at all levels. As a developer, you must manage it well in the micro level, the macro level, and all levels in between.






