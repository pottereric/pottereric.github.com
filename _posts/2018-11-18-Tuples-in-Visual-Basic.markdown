---
comments: true
date: 2018-11-14 4:00:00
layout: post
slug: tuples-in-visual-basic
title: "Tuples in Visual Basic"
summary: "Investigating the syntax for tuples in VB.Net"
image: 'tuples-in-visual-basic\lead.png' 
tags:
- VBNet
---

The new tuple syntax that was added to C# in C#7 has made my code cleaner and more expressive. It isn't a feature that I use every day. But when there are multiple values that need to be moved as a single unit, it is very nice. And it is a big upgrade over the older generic tuple that always had its members named Item1 and Item2. While the generic tuple was useful for creating lightweight groupings, it hurt the readability of the code when the items had to be reference. The new tuples can have custom names, meaning you get the benefits of tuples without sacrificing readability.

While I spent most of my professional development time in C#, it maintain multiple apps written in VB.Net. While the VB team has made a [stategic decision](https://blogs.msdn.microsoft.com/dotnet/2017/02/01/the-net-language-strategy/) to make thier language more stable, they did add support for tuples in the most recent version. I used VB tuples for the first time recently and I am impressed with how clean the syntax is.


### Declaring a Tuple ###
To declare a tuple, all you need to do is wrap two or more values in parentheses. In the following example, the code on line 2 is creating a tuple containing 42 and 84. Using this syntax, the items are still named "Item1" and "Item2" 

<!-- HTML generated using hilite.me --><div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><table><tr><td><pre style="margin: 0; line-height: 125%">1
2
3
4
5</pre></td><td><pre style="margin: 0; line-height: 125%"><span style="color: #008800; font-weight: bold">Function</span> <span style="color: #0066BB; font-weight: bold">UseATuple</span>() <span style="color: #000000; font-weight: bold">As</span> <span style="color: #333399; font-weight: bold">Integer</span>
    <span style="color: #008800; font-weight: bold">Dim</span> pair <span style="color: #333333">=</span> (<span style="color: #0000DD; font-weight: bold">42</span>, <span style="color: #0000DD; font-weight: bold">84</span>)

    <span style="color: #008800; font-weight: bold">Return</span> pair.Item1
<span style="color: #008800; font-weight: bold">End</span> <span style="color: #008800; font-weight: bold">Function</span>
</pre></td></tr></table></div>

The preferred way to declare tuples requires a bit more syntax, but it allows you to specify the names of the members. Using the colon equals syntax, line 2 is decalre a tuple with the same values as above, by now the items can be referenced with their identifiers, Magnitude and Direction. Line 4 uses one of the identifiers. The piece that you can't see in a code sample is that the Visual Studio Intellisense is aware of the identifiers and will list them as autocompletion options.

<!-- HTML generated using hilite.me --><div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><table><tr><td><pre style="margin: 0; line-height: 125%">1
2
3
4
5</pre></td><td><pre style="margin: 0; line-height: 125%"><span style="color: #008800; font-weight: bold">Function</span> <span style="color: #0066BB; font-weight: bold">UseANamedTuple</span>() <span style="color: #000000; font-weight: bold">As</span> <span style="color: #333399; font-weight: bold">Integer</span>
    <span style="color: #008800; font-weight: bold">Dim</span> vector <span style="color: #333333">=</span> (Magnitude:<span style="color: #333333">=</span><span style="color: #0000DD; font-weight: bold">42</span>, Direction:<span style="color: #333333">=</span><span style="color: #0000DD; font-weight: bold">84</span>)

    <span style="color: #008800; font-weight: bold">Return</span> vector.Magnitude
<span style="color: #008800; font-weight: bold">End</span> <span style="color: #008800; font-weight: bold">Function</span>
</pre></td></tr></table></div>

### Passing Tuples ###

The most common use case for tuples is returning multiple values from a function. Without Tuples, you would have to decide between returning one of the values as an out parameter or creating a small data structure to contain them. To return a tuple for a function in VB, all you have to do is specfy the members of the tuple in the method signature, again wrapping them in parenteheses. The names are actuall optional, but I would strongly recomend giving each member a name.

<!-- HTML generated using hilite.me --><div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><table><tr><td><pre style="margin: 0; line-height: 125%">1
2
3</pre></td><td><pre style="margin: 0; line-height: 125%"><span style="color: #008800; font-weight: bold">Function</span> <span style="color: #0066BB; font-weight: bold">ReturnATuple</span>(value <span style="color: #000000; font-weight: bold">As</span> <span style="color: #333399; font-weight: bold">Integer</span>) <span style="color: #000000; font-weight: bold">As</span> (passed <span style="color: #000000; font-weight: bold">As</span> <span style="color: #333399; font-weight: bold">Boolean</span>, result <span style="color: #000000; font-weight: bold">As</span> <span style="color: #333399; font-weight: bold">Integer</span>)
    <span style="color: #008800; font-weight: bold">Return</span> (<span style="color: #008800; font-weight: bold">True</span>, value)
<span style="color: #008800; font-weight: bold">End</span> <span style="color: #008800; font-weight: bold">Function</span>
</pre></td></tr></table></div>


If you need to pass a tuple to a function, the syntax looks similar to the other cases. The tuple declaration is an parameter. The only difference is that you do have to specify an identifier for the tuple. 

<!-- HTML generated using hilite.me --><div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><table><tr><td><pre style="margin: 0; line-height: 125%">1
2
3
4
5
6
7</pre></td><td><pre style="margin: 0; line-height: 125%"><span style="color: #008800; font-weight: bold">Function</span> <span style="color: #0066BB; font-weight: bold">PassATuple</span>(pair <span style="color: #000000; font-weight: bold">As</span> (isValid <span style="color: #000000; font-weight: bold">As</span> <span style="color: #333399; font-weight: bold">Boolean</span>, value <span style="color: #000000; font-weight: bold">As</span> <span style="color: #333399; font-weight: bold">Integer</span>)) <span style="color: #000000; font-weight: bold">As</span> <span style="color: #333399; font-weight: bold">Integer</span>
    <span style="color: #008800; font-weight: bold">If</span> pair.isValid <span style="color: #008800; font-weight: bold">Then</span>
        <span style="color: #008800; font-weight: bold">Return</span> pair.value
    <span style="color: #008800; font-weight: bold">Else</span>
        <span style="color: #008800; font-weight: bold">Return</span> <span style="color: #0000DD; font-weight: bold">0</span>
    <span style="color: #008800; font-weight: bold">End</span> <span style="color: #008800; font-weight: bold">If</span>
<span style="color: #008800; font-weight: bold">End</span> <span style="color: #008800; font-weight: bold">Function</span>
</pre></td></tr></table></div>


