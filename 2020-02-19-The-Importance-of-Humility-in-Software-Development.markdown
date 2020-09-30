---
comments: true
date: 2020-02-19 4:00:00
layout: post
slug: the-importance-of-humility-in-software-development
title: "The Importance of Humility in Software Development"
summary: "We need to be mindful of our cognitive limitations."
image: 'the-importance-of-humility-in-software-development\lead.png' 
tags:
- Humility
---

All too frequently, we hear news of another major software bug. Bugs from big companies make the biggest news. Bugs from little companies seem just as common. As programmers, all these bugs are costing us time and money. We know we need to improve. But we can't seem to figure out how.

As an industry, we've tried solving this problem with increasingly complex processes, increasingly complex tools, and sophisticated techniques. But Edsger Dijkstra proposed a different, simpler solution. 

Dijkstra was one of the early pioneers of software development. He made important contributions in compilers, operating systems, and distributed systems. But he didn't claim that advances in these areas would lead to more reliable software. What he thought would make the most significant difference was humility. 

In his 1972 [ACM Turing Award lecture](https://www.cs.utexas.edu/~EWD/transcriptions/EWD03xx/EWD340.html), he described the process he envisioned for consistently delivering high-quality software. He saw the 3 keys to this revolution
1. The use of abstraction to make programs intellectually manageable
2. Developing correctness proofs alongside the software
3. Approaching the task of software development as humble programmers

Why did he think that humility was a critical component? Let's look at the key passage in the lecture:

> Now for the fifth argument. It has to do with the influence of the tool we are trying to use upon our own thinking habits. I observe a cultural tradition, which in all probability has its roots in the Renaissance, to ignore this influence, to regard the human mind as the supreme and autonomous master of its artefacts. But if I start to analyse the thinking habits of myself and of my fellow human beings, I come, whether I like it or not, to a completely different conclusion, viz. that the tools we are trying to use and the language or notation we are using to express or record our thoughts, are the major factors determining what we can think or express at all! The analysis of the influence that programming languages have on the thinking habits of its users, and the recognition that, by now, **brainpower is by far our scarcest resource**, they together give us a new collection of yardsticks for comparing the relative merits of various programming languages. **The competent programmer is fully aware of the strictly limited size of his own skull; therefore he approaches the programming task in full humility**, and among other things he avoids clever tricks like the plague. 

Dijkstra reminds us that our brains are not perfect computing machines. We must not treat them as if they were. We must be open to the possibility at all times that we have made a mistake. Dijkstra is not saying that we should act like we are morons. He's saying that we need to remember our limitations.

Let me be clear. I'm not trying to reinforce impostor syndrome. I'm not advocating for intellectual gatekeeping. You can be an excellent developer and still need to be mindful of your limitations. In fact, in a true and seemingly paradoxical way, healthy humility can help you go from being a good programmer to a great one.

He says, "brainpower is by far our scarcest resource." He said that back in 1972. How much more true is that statement today with our modern computers, programming languages, IDEs, and associated tools. 

He goes on to explain why our limited brainpower makes well-factored code so critical. 

> The best way to learn to live with our limitations is to know them. By the time that we are sufficiently modest to try factored solutions only, because the other efforts escape our intellectual grip, we shall do our utmost best to avoid all those interfaces impairing our ability to factor the system in a helpful way.



TODO: Write up some action items

- naming
- pairing / code reviews
- testing

In his conclusion, he points out that we need to be mindful of both the complexities of software development and the limitations of our abilities. 

> We shall do a much better programming job, provided that we approach the task with a full appreciation of its tremendous difficulty, provided that we stick to modest and elegant programming languages, **provided that we respect the intrinsic limitations of the human mind and approach the task as Very Humble Programmers**.

