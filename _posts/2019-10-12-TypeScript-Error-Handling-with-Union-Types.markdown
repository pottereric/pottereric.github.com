---
comments: true
date: 2019-10-12 4:00:00
layout: post
slug: typescript-error-handling-with-union-types
title: "TypeScript Error Handling with Union Types"
summary: "TypeScript functions can return Union Types to cleanly indicate error conditions."
image: 'typescript-error-handling-with-union-types\lead.png' 
tags:
- TypeScript
---

One of the challenges of modern software development is handling errors in elegant ways. Fortunately for TypeScript users, there is a clean way to indicate whether or not a function encountered an error by using Union Types.

Let’s consider an simple example where there is a table in a database that contains information about programmers. We have a function that intends to take the programmer's name as an argument, lookup the programmer in the database, and return the programmer’s favorite programming language. In an ideal world, the code could look like this. (The actual database lookup has been omitted for brevity.)


<!-- HTML generated using hilite.me --><div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><table><tr><td><pre style="margin: 0; line-height: 125%"> 1
 2
 3
 4
 5
 6
 7
 8
 9
10
11
12
13
14
15</pre></td><td ><pre style="margin: 0; line-height: 125%"><span style="color: #008800; font-weight: bold">import</span> {Programmer} from <span style="background-color: #fff0f0">&quot;./Programmer&quot;</span>

<span style="color: #008800; font-weight: bold">export</span> <span style="color: #008800; font-weight: bold">class</span> ProgrammerRepository{
    <span style="color: #008800; font-weight: bold">public</span> GetByName(name : <span style="color: #333399; font-weight: bold">String</span>) <span style="color: #333333">:</span> Programmer{
        <span style="color: #888888">// stub for more interesting data retrieval</span>
        <span style="color: #008800; font-weight: bold">return</span> <span style="color: #008800; font-weight: bold">new</span> Programmer(<span style="background-color: #fff0f0">&quot;Robert Tables&quot;</span>, <span style="background-color: #fff0f0">&quot;TypeScript&quot;</span>);
    }
}

<span style="color: #888888">// Client Code //</span>

<span style="color: #008800; font-weight: bold">export</span> <span style="color: #008800; font-weight: bold">function</span> GetFavoriteLanguage(name : <span style="color: #333399; font-weight: bold">String</span>) <span style="color: #333333">:</span> <span style="color: #007020">String</span>{
    <span style="color: #008800; font-weight: bold">var</span> repo <span style="color: #333333">=</span> <span style="color: #008800; font-weight: bold">new</span> ProgrammerRepository();
    <span style="color: #008800; font-weight: bold">return</span> repo.GetByName(name).GetFavoriteLanguage();
}
</pre></td></tr></table></div>


This code is simple and straightforward, but it doesn’t do anything to handle error cases. As any experienced programmer knows, looking up data in a database can fail in a large number of ways. 


<h2>Throwing Errors</h2>

The traditional way to handle failures in JavaScript is to throw Errors. In our simplified example, this would mean that if the repository code couldn’t connect to the database, couldn’t find the record in the database, or some related error, the repository would throw an Error.


<!-- HTML generated using hilite.me --><div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><table><tr><td><pre style="margin: 0; line-height: 125%"> 1
 2
 3
 4
 5
 6
 7
 8
 9
10
11
12
13
14
15
16
17
18
19
20
21
22</pre></td><td><pre style="margin: 0; line-height: 125%"><span style="color: #008800; font-weight: bold">import</span> {Programmer} from <span style="background-color: #fff0f0">&quot;./Programmer&quot;</span>

<span style="color: #008800; font-weight: bold">export</span> <span style="color: #008800; font-weight: bold">class</span> ProgrammerRepository{
    <span style="color: #008800; font-weight: bold">public</span> GetByName(name : <span style="color: #333399; font-weight: bold">String</span>) <span style="color: #333333">:</span> Programmer{
        <span style="color: #888888">// stub for more interesting data retrieval</span>
        <span style="color: #008800; font-weight: bold">throw</span> <span style="color: #008800; font-weight: bold">new</span> <span style="color: #007020">Error</span>(<span style="background-color: #fff0f0">&quot;data storage error&quot;</span>);
    }
}

<span style="color: #888888">// Client Code //</span>

<span style="color: #008800; font-weight: bold">export</span> <span style="color: #008800; font-weight: bold">function</span> GetFavoriteLanguage(name : <span style="color: #333399; font-weight: bold">String</span>) <span style="color: #333333">:</span> <span style="color: #007020">String</span>{
    <span style="color: #008800; font-weight: bold">var</span> repo <span style="color: #333333">=</span> <span style="color: #008800; font-weight: bold">new</span> ProgrammerRepository();
    <span style="color: #008800; font-weight: bold">var</span> favLang : <span style="color: #333399; font-weight: bold">String</span>;

    <span style="color: #008800; font-weight: bold">try</span>{
        favLang <span style="color: #333333">=</span> repo.GetByName(name).GetFavoriteLanguage();
    } <span style="color: #008800; font-weight: bold">catch</span> {
        favLang <span style="color: #333333">=</span> <span style="background-color: #fff0f0">&quot;Could not be found&quot;</span>
    }
    <span style="color: #008800; font-weight: bold">return</span> favLang;
}
</pre></td></tr></table></div>

This implementation of GetByName will throw an Error if the lookup fails for any reason. This technique functions properly and many developers are used to this style of error handling.  

One potential problem with this style of error handling is that the client code is not forced to handle the error. The client code could ignore the potential exception, which could lead to unhandled exceptions in production. 

A second potential problem is that the signature of the GetByName function does not indicate what kinds of errors might be thrown.

<h2>Returning a Union Type</h2>

The TypeScript type system supports a mechanism called Union Types. Union Types specify that an object will be instance of one of the types that are joined together in the union.

On line 4 of the following example, a union type named ProgrammerLookupResult is defined as the union of Programmer and LookupFailed. All of the instances of ProgrammerLookupResult will either be an instance of a Programmer or an instance of the LookupFailed class. 


<!-- HTML generated using hilite.me --><div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><table><tr><td><pre style="margin: 0; line-height: 125%"> 1
 2
 3
 4
 5
 6
 7
 8
 9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27</pre></td><td><pre style="margin: 0; line-height: 125%"><span style="color: #008800; font-weight: bold">import</span> {Programmer} from <span style="background-color: #fff0f0">&quot;./Programmer&quot;</span>
<span style="color: #008800; font-weight: bold">import</span> {LookupFailed} from <span style="background-color: #fff0f0">&quot;./LookupFailed&quot;</span>

<span style="color: #008800; font-weight: bold">export</span> type ProgrammerLookupResult <span style="color: #333333">=</span> Programmer <span style="color: #333333">|</span> LookupFailed;

<span style="color: #008800; font-weight: bold">export</span> <span style="color: #008800; font-weight: bold">class</span> ProgrammerRepository{
    <span style="color: #008800; font-weight: bold">public</span> GetByName(name : <span style="color: #333399; font-weight: bold">String</span>) <span style="color: #333333">:</span> ProgrammerLookupResult {
        <span style="color: #888888">// stub for more interesting data retrieval</span>
        <span style="color: #008800; font-weight: bold">return</span> <span style="color: #008800; font-weight: bold">new</span> LookupFailed(<span style="background-color: #fff0f0">&quot;Entity not found&quot;</span>);
    }
}

<span style="color: #888888">// Client Code //</span>

<span style="color: #008800; font-weight: bold">export</span> <span style="color: #008800; font-weight: bold">function</span> GetFavoriteLanguage(name : <span style="color: #333399; font-weight: bold">String</span>) <span style="color: #333333">:</span> <span style="color: #007020">String</span>{
    <span style="color: #008800; font-weight: bold">var</span> repo <span style="color: #333333">=</span> <span style="color: #008800; font-weight: bold">new</span> ProgrammerRepository();
    <span style="color: #008800; font-weight: bold">var</span> favLang : <span style="color: #333399; font-weight: bold">String</span> <span style="color: #333333">=</span> <span style="background-color: #fff0f0">&quot;&quot;</span>;

    <span style="color: #008800; font-weight: bold">let</span> result <span style="color: #333333">=</span> repo.GetByName(name);
    
    <span style="color: #008800; font-weight: bold">if</span>(result <span style="color: #008800; font-weight: bold">instanceof</span> Programmer){
        favLang <span style="color: #333333">=</span> result.GetFavoriteLanguage();
    } <span style="color: #008800; font-weight: bold">else</span> <span style="color: #008800; font-weight: bold">if</span> (result <span style="color: #008800; font-weight: bold">instanceof</span> LookupFailed) {
        favLang <span style="color: #333333">=</span> <span style="background-color: #fff0f0">&quot;Could not be found&quot;</span>;
    }
    <span style="color: #008800; font-weight: bold">return</span> favLang;
}
</pre></td></tr></table></div>

This implementation of GetByName returns an instance of ProgrammerLookupResult. If the lookup succeeded, it will be an instance of Programmer. Otherwise it will be an instance of LookupFailed.

The first thing to note is that TypeScript will not allow the client code to access the Programmer specific methods, like GetFavoriteLanguage until the type has been checked with a Type Guard. On line 21 of this example, the function checks the type of result. If this evaluates to true, the code on line 22 can call GetFavoriteLanguage without getting a compiler error. 

This solves the two potential problems posed by the implementation with throwing Errors. The client code must check the type of the result, otherwise he code cannot compile. This results in fewer unhandled errors. Secondly, because it is easy to look at the definition of the union, it is clear to the developer writing the client code exactly which kinds of errors can be returned.

It is worth noting that the union type could be defined in line with the function. This would work identically to the previous example and it would make the code slightly shorter. I prefer to have the union type defined explicitly since in makes the intent of the union type clearer.

<!-- HTML generated using hilite.me --><div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><table><tr><td><pre style="margin: 0; line-height: 125%">1
2
3
4
5
6</pre></td><td><pre style="margin: 0; line-height: 125%"><span style="color: #008800; font-weight: bold">export</span> <span style="color: #008800; font-weight: bold">class</span> ProgrammerRepository{
    <span style="color: #008800; font-weight: bold">public</span> GetByName(name : <span style="color: #333399; font-weight: bold">String</span>) <span style="color: #333333">:</span> Programmer <span style="color: #333333">|</span> LookupFailed {
        <span style="color: #888888">// stub for more interesting data retrieval</span>
        <span style="color: #008800; font-weight: bold">return</span> <span style="color: #008800; font-weight: bold">new</span> LookupFailed(<span style="background-color: #fff0f0">&quot;Entity not found&quot;</span>);
    }
}
</pre></td></tr></table></div>



<h2>Conclusion</h2>

Using Union Types to return errors from functions makes it clear to their clients what errors might be encountered. It guides them in how the potential errors must be handled. The result is more reliable software with fewer unhandled errors.

To view all code used in this post, please visit the GitHub [repository](https://github.com/pottereric/TypeScriptErrorHandling). 