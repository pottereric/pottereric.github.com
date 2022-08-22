---
comments: true
date: 2019-12-21 4:00:00
layout: post
slug: csharp-strings-with-ranges,-and-indexes
title: "C# Strings with Ranges, and Indexes"
summary: "Using the range and index operators to manipulate strings in C#8"
image: 'csharp-strings-with-ranges,-and-indexes\lead.png' 
tags:
- CSharp
---

>  This blog post is part of Third C# Annual Advent organized by Matt Groves, Developer Advocate Couchbase and Microsoft MVP. Thanks to Matt for giving me an opportunity to participate again this year. You can follow the C# Advent [here](https://crosscuttingconcerns.com/). 

C# 8 introduced the ability to access subsets of collections with range operators. Frequently, ranges are used to access arrays or spans, but they can also be used to access the characters inside a string. This can be especially useful if you know there are fixed length portions of text within the string you are manipulating. 

For example, let's say that you wanted to get the first eight characters of a file name. You could use the Substring method on the string class. Or you could use a range operator to get the first eight characters. 

<pre style="font-family:InputMono;font-size:15px;color:gainsboro;background:#1e1e1e;"><span style="color:yellowgreen;">[</span><span style="color:#4ec9b0;">TestMethod</span><span style="color:yellowgreen;">]</span>
<span style="color:#569cd6;">public</span>&nbsp;<span style="color:#569cd6;">void</span>&nbsp;<span style="font-weight:bold;color:#dcdcaa;">GetTheFirstEightCharactersOfAString</span><span style="color:yellowgreen;">()</span>
<span style="color:yellowgreen;">{</span>
&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#569cd6;">string</span>&nbsp;<span style="font-weight:bold;color:#9cdcfe;">fileName</span>&nbsp;<span style="color:#b4b4b4;">=</span>&nbsp;<span style="color:#d69d85;">&quot;myTestFileName.txt&quot;</span>;
&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#569cd6;">string</span>&nbsp;<span style="font-weight:bold;color:#9cdcfe;">firstEight</span>&nbsp;<span style="color:#b4b4b4;">=</span>&nbsp;<span style="font-weight:bold;color:#9cdcfe;">fileName</span><span style="color:darkviolet;">[</span><span style="color:#b5cea8;">0</span>..<span style="color:#b5cea8;">8</span><span style="color:darkviolet;">]</span>;
&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#4ec9b0;">Assert</span><span style="color:#b4b4b4;">.</span><span style="font-weight:bold;color:#dcdcaa;">AreEqual</span><span style="color:darkviolet;">(</span><span style="color:#d69d85;">&quot;myTestFi&quot;</span>,&nbsp;<span style="font-weight:bold;color:#9cdcfe;">firstEight</span><span style="color:darkviolet;">)</span>;
<span style="color:yellowgreen;">}</span>
</pre>

Because the range starts at the beginning of the collection of characters in the string, the first 0 in the range is optional. You could achieve the same this by leaving it out. 

<pre style="font-family:InputMono;font-size:15px;color:gainsboro;background:#1e1e1e;"><span style="color:yellowgreen;">[</span><span style="color:#4ec9b0;">TestMethod</span><span style="color:yellowgreen;">]</span>
<span style="color:#569cd6;">public</span>&nbsp;<span style="color:#569cd6;">void</span>&nbsp;<span style="font-weight:bold;color:#dcdcaa;">GetTheFirstEightCharactersOfAString_Shorter</span><span style="color:yellowgreen;">()</span>
<span style="color:yellowgreen;">{</span>
&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#569cd6;">string</span>&nbsp;<span style="font-weight:bold;color:#9cdcfe;">fileName</span>&nbsp;<span style="color:#b4b4b4;">=</span>&nbsp;<span style="color:#d69d85;">&quot;myTestFileName.txt&quot;</span>;
&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#569cd6;">string</span>&nbsp;<span style="font-weight:bold;color:#9cdcfe;">firstEight</span>&nbsp;<span style="color:#b4b4b4;">=</span>&nbsp;<span style="font-weight:bold;color:#9cdcfe;">fileName</span><span style="color:darkviolet;">[</span>..<span style="color:#b5cea8;">8</span><span style="color:darkviolet;">]</span>;
&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#4ec9b0;">Assert</span><span style="color:#b4b4b4;">.</span><span style="font-weight:bold;color:#dcdcaa;">AreEqual</span><span style="color:darkviolet;">(</span><span style="color:#d69d85;">&quot;myTestFi&quot;</span>,&nbsp;<span style="font-weight:bold;color:#9cdcfe;">firstEight</span><span style="color:darkviolet;">)</span>;
<span style="color:yellowgreen;">}</span>
</pre>

What would be more likely is that you would want to get the file name without the extension. Assuming that you know with certainty that the file extension will always be three characters, you could define a range the starts at the beginning of the string and ends four characters from the end. You do this by using the caret to indicate that an index counts from the back of the collection. So a range of [0..^4] would retrieve all but the last four characters, which in this case would be the file name without ".txt".

<pre style="font-family:InputMono;font-size:15px;color:gainsboro;background:#1e1e1e;"><span style="color:yellowgreen;">[</span><span style="color:#4ec9b0;">TestMethod</span><span style="color:yellowgreen;">]</span>
<span style="color:#569cd6;">public</span>&nbsp;<span style="color:#569cd6;">void</span>&nbsp;<span style="font-weight:bold;color:#dcdcaa;">GetTheFileNameWithoutTheExtension</span><span style="color:yellowgreen;">()</span>
<span style="color:yellowgreen;">{</span>
&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#569cd6;">string</span>&nbsp;<span style="font-weight:bold;color:#9cdcfe;">fileName</span>&nbsp;<span style="color:#b4b4b4;">=</span>&nbsp;<span style="color:#d69d85;">&quot;myTestFileName.txt&quot;</span>;
&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#569cd6;">string</span>&nbsp;<span style="font-weight:bold;color:#9cdcfe;">fileNameWithExtension</span>&nbsp;<span style="color:#b4b4b4;">=</span>&nbsp;<span style="font-weight:bold;color:#9cdcfe;">fileName</span><span style="color:darkviolet;">[</span><span style="color:#b5cea8;">0</span>..<span style="color:#b4b4b4;">^</span><span style="color:#b5cea8;">4</span><span style="color:darkviolet;">]</span>;
&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#4ec9b0;">Assert</span><span style="color:#b4b4b4;">.</span><span style="font-weight:bold;color:#dcdcaa;">AreEqual</span><span style="color:darkviolet;">(</span><span style="color:#d69d85;">&quot;myTestFileName&quot;</span>,&nbsp;<span style="font-weight:bold;color:#9cdcfe;">fileNameWithExtension</span><span style="color:darkviolet;">)</span>;
<span style="color:yellowgreen;">}</span></pre>

If you wanted to only get the file extension, you could define a range in which both indexes in the range count from the back. A range defined from ^3 to ^0 would get the last three characters in the string. Assuming again that you know that the extension is three characters, this would get the extension. 

<pre style="font-family:InputMono;font-size:15px;color:gainsboro;background:#1e1e1e;"><span style="color:yellowgreen;">[</span><span style="color:#4ec9b0;">TestMethod</span><span style="color:yellowgreen;">]</span>
<span style="color:#569cd6;">public</span>&nbsp;<span style="color:#569cd6;">void</span>&nbsp;<span style="font-weight:bold;color:#dcdcaa;">GetTheExtension</span><span style="color:yellowgreen;">()</span>
<span style="color:yellowgreen;">{</span>
&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#569cd6;">string</span>&nbsp;<span style="font-weight:bold;color:#9cdcfe;">fileName</span>&nbsp;<span style="color:#b4b4b4;">=</span>&nbsp;<span style="color:#d69d85;">&quot;myTestFileName.txt&quot;</span>;
&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#569cd6;">string</span>&nbsp;<span style="font-weight:bold;color:#9cdcfe;">extension</span>&nbsp;<span style="color:#b4b4b4;">=</span>&nbsp;<span style="font-weight:bold;color:#9cdcfe;">fileName</span><span style="color:darkviolet;">[</span><span style="color:#b4b4b4;">^</span><span style="color:#b5cea8;">3</span>..<span style="color:#b4b4b4;">^</span><span style="color:#b5cea8;">0</span><span style="color:darkviolet;">]</span>;
&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#4ec9b0;">Assert</span><span style="color:#b4b4b4;">.</span><span style="font-weight:bold;color:#dcdcaa;">AreEqual</span><span style="color:darkviolet;">(</span><span style="color:#d69d85;">&quot;txt&quot;</span>,&nbsp;<span style="font-weight:bold;color:#9cdcfe;">extension</span><span style="color:darkviolet;">)</span>;
<span style="color:yellowgreen;">}</span>
</pre>

In the same way that we can omit the number for the beginning of the range if the range starts at the beginning of the collection, we can omit the number at the end of the range if the range ends at the end of the collection. This code would also retrieve the extension of the file, but is slightly shorter. 

<pre style="font-family:InputMono;font-size:15px;color:gainsboro;background:#1e1e1e;"><span style="color:yellowgreen;">[</span><span style="color:#4ec9b0;">TestMethod</span><span style="color:yellowgreen;">]</span>
<span style="color:#569cd6;">public</span>&nbsp;<span style="color:#569cd6;">void</span>&nbsp;<span style="font-weight:bold;color:#dcdcaa;">GetTheExtension_Shorter</span><span style="color:yellowgreen;">()</span>
<span style="color:yellowgreen;">{</span>
&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#569cd6;">string</span>&nbsp;<span style="font-weight:bold;color:#9cdcfe;">fileName</span>&nbsp;<span style="color:#b4b4b4;">=</span>&nbsp;<span style="color:#d69d85;">&quot;myTestFileName.txt&quot;</span>;
&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#569cd6;">string</span>&nbsp;<span style="font-weight:bold;color:#9cdcfe;">extension</span>&nbsp;<span style="color:#b4b4b4;">=</span>&nbsp;<span style="font-weight:bold;color:#9cdcfe;">fileName</span><span style="color:darkviolet;">[</span><span style="color:#b4b4b4;">^</span><span style="color:#b5cea8;">3</span>..<span style="color:darkviolet;">]</span>;
&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#4ec9b0;">Assert</span><span style="color:#b4b4b4;">.</span><span style="font-weight:bold;color:#dcdcaa;">AreEqual</span><span style="color:darkviolet;">(</span><span style="color:#d69d85;">&quot;txt&quot;</span>,&nbsp;<span style="font-weight:bold;color:#9cdcfe;">extension</span><span style="color:darkviolet;">)</span>;
<span style="color:yellowgreen;">}</span>
</pre>

Lets say that you have a string that is wrapped in curly braces and you only want the text inside the braces. You could easily define a range that leaves off the first and last character of the string. 

<pre style="font-family:InputMono;font-size:15px;color:gainsboro;background:#1e1e1e;"><span style="color:yellowgreen;">[</span><span style="color:#4ec9b0;">TestMethod</span><span style="color:yellowgreen;">]</span>
<span style="color:#569cd6;">public</span>&nbsp;<span style="color:#569cd6;">void</span>&nbsp;<span style="font-weight:bold;color:#dcdcaa;">GetTextInsideOfBrackets</span><span style="color:yellowgreen;">()</span>
<span style="color:yellowgreen;">{</span>
&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#569cd6;">string</span>&nbsp;<span style="font-weight:bold;color:#9cdcfe;">data</span>&nbsp;<span style="color:#b4b4b4;">=</span>&nbsp;<span style="color:#d69d85;">&quot;{importantData}&quot;</span>;
&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#569cd6;">string</span>&nbsp;<span style="font-weight:bold;color:#9cdcfe;">innerData</span>&nbsp;<span style="color:#b4b4b4;">=</span>&nbsp;<span style="font-weight:bold;color:#9cdcfe;">data</span><span style="color:darkviolet;">[</span><span style="color:#b5cea8;">1</span>..<span style="color:#b4b4b4;">^</span><span style="color:#b5cea8;">1</span><span style="color:darkviolet;">]</span>;
&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#4ec9b0;">Assert</span><span style="color:#b4b4b4;">.</span><span style="font-weight:bold;color:#dcdcaa;">AreEqual</span><span style="color:darkviolet;">(</span><span style="color:#d69d85;">&quot;importantData&quot;</span>,&nbsp;<span style="font-weight:bold;color:#9cdcfe;">innerData</span><span style="color:darkviolet;">)</span>;
<span style="color:yellowgreen;">}</span>
</pre>

Using the range operators to access substring of strings doesn't radically shift the paradigm of your code. But it does make it easier to do some of the operations that we have to write on regular basis. If you have any good examples of how you have used ranges to work with strings, please let me know in the comments below. 

It you want to play with the code from this post, you can find it [here](https://github.com/pottereric/CSharpStringsRangesAndIndexes).
