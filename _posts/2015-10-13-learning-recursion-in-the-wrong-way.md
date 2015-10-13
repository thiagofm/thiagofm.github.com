---
layout: post
title: "Learning recursion in the wrong way"
description: ""
category: scip
tags: ["functional-programming fp scheme scip"]
---
{% include JB/setup %}

I've been reading **Structure and Interpretation of Computer Programs**(the one that has a wizard in the book cover). It's impressive how well-written it is and how it increments well from what I've been taught in other books and mainly at university.

![SCIP]({{ site.url }}/assets/images/scip.jpg)

At university, we refered recursion, recursive, anything that has the recur prefix as a function which calls itself. And also made some funny jokes such as "To understand recursion, you must understand recursion.". But that was it.

In programming books there's always a mention if the language supports tail call optimization, tail call. But it's usually pragmatic about what the concept of recursion. Every "recursive" example is usually about a function calling itself.

SCIP teaches you the basics of Scheme in the very first pages but then, uses the word "iteration" for a procedure that calls itself. Wat.

But then, later in the book, after you wrote a couple of "iterative" procedures, it raises up the recursion naming debate and litelly kills it. And then I wanted to share this in a blogpost, of course.

> In contrasting iteration and recursion, we must be careful not to confuse the notion of a recursive process with the notion of a recursive procedure. When we describe a procedure as recursive, we are referring to the syntactic fact that the procedure definition refers (either directly or indirectly) to the procedure itself. But when we describe a process as following a pattern that is, say, linearly recursive, we are speaking about how the process evolves, not about the syntax of how a procedure is written. It may seem disturbing that we refer to a recursive procedure such as fact-iter as generating an iterative process. However, the process really is iterative: Its state is captured completely by its three state variables, and an interpreter need keep track of only three variables in order to execute the process.

Small observation: If you need a bit more of context, you can read the whole reasoning [here](https://mitpress.mit.edu/sicp/full-text/sicp/book/node15.html).

This is also a sweet way to introduce about tail call optimization. TCO-able functions are the functions that are a recursive procedure, but still a iterative proccess.
