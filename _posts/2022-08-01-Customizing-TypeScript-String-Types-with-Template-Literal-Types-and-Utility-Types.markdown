---
comments: true
date: 2022-08-01 4:00:00
layout: post
slug: customizing-typescript-string-types-with-template-literal-types-and-utility-types
title: "Customizing TypeScript String Types with Template Literal Types and Utility Types"
summary: "TODO teset"
image: 'customizing-typescript-string-types-with-template-literal-types-and-utility-types\lead.png' 
tags:
- TypeScript
---

TypeScript has an interesting feature that lets you define a type for a subset of valid strings. These are called String Literal Types. String Literals are a special kind of Union Type. At first glance, this looks similar to an enumeration. But enumerations use numbers as their underlying storage. String Literals maintains all of the behavior of strings. 

[![](/img/posts/customizing-typescript-string-types-with-template-literal-types-and-utility-types/String Literals.png)](/img/posts/customizing-typescript-string-types-with-template-literal-types-and-utility-types/String Literals.png)

If I define a String Literal as I did on line 1 above, I have a type, named Grade, that can only be 'A', 'B', 'C', 'D', or 'F'. So if I try to pass an 'E' as an argument to function that takes a Grade as a parameter, I will get a compiler error, as shown on line 8 in the example below.

It is important to remember that these checks are only run at compile time and cannot be used directly for run-time concerns like input validation.

[![](/img/posts/customizing-typescript-string-types-with-template-literal-types-and-utility-types/String Literals Usage.png)](/img/posts/customizing-typescript-string-types-with-template-literal-types-and-utility-types/String Literals Usage.png)

String Literal Types can be very useful when writing DOM manipulation functions. You may have a function that is designed to only work with a subset of tags. You could create a String Literal type for that subset and ensure the function is only called with the appropriate tag names.

### Template Literal Types

[Template Literal Types](https://www.typescriptlang.org/docs/handbook/2/template-literal-types.html), introduced in TypeScript 4.1, take this concept even further. Instead of needing to specify every valid value, they can be generated from String Literals. In the example below, we define a second String Literal called GradeModifiers. Then we use a Template Literal on line 18 to generate every possible combination of Grade and GradeModifier. 

[![](/img/posts/customizing-typescript-string-types-with-template-literal-types-and-utility-types/Template Literal Types.png)](/img/posts/customizing-typescript-string-types-with-template-literal-types-and-utility-types/Template Literal Types.png)

As you can see on line 13 in the code example below, we can now enter 'B+' as a valid grade, which is great. But we can also pass 'F-', which we don't want to allow.

[![](/img/posts/customizing-typescript-string-types-with-template-literal-types-and-utility-types/Template Literal Types Usage.png)](/img/posts/customizing-typescript-string-types-with-template-literal-types-and-utility-types/Template Literal Types Usage.png)

As you can see from the Intellisense pictured below, the expandedGrades type that we generated with a Template Literal generate every possible combination, which include 'F+' and 'F-'. So how do we exclude them?

[![](/img/posts/customizing-typescript-string-types-with-template-literal-types-and-utility-types/Template Literal Types Result.png)](/img/posts/customizing-typescript-string-types-with-template-literal-types-and-utility-types/Template Literal Types Result.png)

### Utility Types

TypeScript also provides tools to customize type definitions called [Utility Types](https://www.typescriptlang.org/docs/handbook/utility-types.html#excludeuniontype-excludedmembers). For our purpose we want to use the Exclude operator, which can remove items from a Union Type. Since String Literals are Union Types, we can use the Exclude operator to exclude 'F+' and 'F-' from our list, as pictured below on line 20. 

[![](/img/posts/customizing-typescript-string-types-with-template-literal-types-and-utility-types/Utility Types.png)](/img/posts/customizing-typescript-string-types-with-template-literal-types-and-utility-types/Utility Types.png)

With our function definition updated to use our improved type, we can still pass 'B+' as before. But we now get a compiler error if we try to pass 'F-'

[![](/img/posts/customizing-typescript-string-types-with-template-literal-types-and-utility-types/Utility Types Usage.png)](/img/posts/customizing-typescript-string-types-with-template-literal-types-and-utility-types/Utility Types Usage.png)

Thanks to the guy at That Conference who was in my session on Advanced Features of the TypeScript type system that told me about this possible combination. It was a cool moment where I got to learn something in the middle of teaching. Thank you!
