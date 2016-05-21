---
title: "Practical Refactoring"
layout: post
date: 2016-05-02 22:44
blog: true
star: true
---

#Practical Refactoring

https://www.youtube.com/watch?v=aWiwDdx_rdo&ab_channel=LlewellynFalco

Source code is java: http://presentations.codeplex.com/SourceControl/latest

###Simple techniques for code excellence.

>What is legacy code? Any code we want to keep, that works, we want to keep working.
Two Cars example. No rewrite. Different path. Happy and proud. Refer to title.
Code excellence is more about discipline that brilliance.

refactor in 2 mins  - never more than 2 mins to check in - run test every two mins

###When to refactor?
refactor when you see code that is hard to understand.
Spend the time you would have taken understanding it to refactor it. Then the refactor is free.
Now you have code that expresses its’ purpose, you just have to read it.
The goal of refactoring is to make code more understandable.

#Three C's

###Remove clutter
- anything that doesn't add understanding or clarity
- bad formatting
- useless comments
- magic numbers

###Remove complexity

Big methods "In every big method there are small classes waiting to get out"
- don't try to understand
- extract new methods, pull out scopes -> grab it by the curlyies (seams)
- undo extractions and fix incorrect scoping as it emerges
- Multiple return values problem - create a data object to return
- Rename as the code becomes clear - composing the method

###Remove cleverness
encapsulate cleverness (hide mess under rug)

#Three D's
###duplication, duplication, duplication
- fold all methods up
- take a look at the names
- group similar methods to find the classes within
- dry out code with polymorphism

###Refactoring procedural code to Good OO code
Group methods by names
- group by arguments
- group by instance variables
1. create class - move grouped methods  (look how code is now more robust) SR
5. if classes have similar purposes, make the method signatures identical, extract interface / base class OC LS IS
7. Invert dependencies -> remove instations from micro-managers (fat controllers?). DI
