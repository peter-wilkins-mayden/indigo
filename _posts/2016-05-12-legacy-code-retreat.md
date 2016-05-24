 ---
 title: "Legacy Code Retreat"
 layout: post
 date: 2016-04-12 22:44
 blog: true
 star: true
 ---

 Legacy Code Retreat
---

[Php Code with golden master test already setup](https://github.com/peter-wilkins-mayden/trivia)

Code Retreats are an opportunity to experiment and learn without the normal pressures of work. There are various exercises to explore different concepts, always on the same code. 45 min sessions with a learning goal, at the end we delete changes and change partner. The aim is not to succeed but to learn (probably from failure) with quick iterations and retro’s.

[Video highlights of a short 2 hour LCR presentation by JB Rainsburger: ](https://www.youtube.com/watch?v=WMsc9tt5jco&ab_channel=agileonthebeach)

>‘I describe refactoring as the act of identifying a specifiic problem with code, envisioning how to improve it, then improving it in small, reversible steps.’

Learn how to do these three things:
 - How to identify code smells
 - How to apply refactorings
 - Which refactorings eliminate which code smells

When you don’t know the impact of a change on the rest of the system, introduce interfaces at the boundary of the code you want to change. Extracting an interface is among the safest structural changes one can make to a code base.

A simple design exhibits these properties:
- It passes all the tests
- It minimizes duplication in all its forms
- It expresses its intent clearly to the reader - “intention-revealing names”
- It removes unnecessary elements

Note that I put these properties in priority order. I’m willing to copy-and-paste to get a test passing, but once the test passes, I can usually remove the duplication quickly. I’m willing to extract code into a method and call it foo() in order to get rid of duplicate code, although that name foo() rarely survives more than 15 minutes. Finally, I will gladly introduce interfaces, classes, methods and variables to clarify the intent of a piece of code, although generally speaking once I make things more clear, I can find things to cut.
removing duplication helps that structure to emerge

improving names helps responsibilities emerge

better structures -> improve names ->  revealing more intent -> finding more duplication -> better names -> abstractions emerge -> higher level patterns emerge -> more duplication ...




1. *safety* Golden master - red flag, test + refactor = chicken + egg, mantra: "That shouldn't have changed anything"

2. State (procedural) = Temporal coupling, not idempotent, variables break ability to reason about code,
refactor to pure functions (start with roll), leave old version but call new one (trivial extract - no structural change - tests still run). Static keyword useful. class var reads to parameters. Class var writes to return value that old func sets to class var. Write struct for multiple returns. Pure func = easy to test, parameters (names) reveal cohesion problems, introduce parameter object, now break down pure function, command query separation violation, this exercise enforces 4 rules simple design.

 What is 'Inheritance to delegation' method?

-------------

Series of tutorials in PHP:

http://tutsplus.com/authors/patkos-csaba

http://code.tutsplus.com/tutorials/refactoring-legacy-code-part-1-the-golden-master--cms-20331

- Magic Strings & Constants
Complex Conditionals -> well named methods (positive question) No Negative Conditionals
- Extract Method Refactoring - isolate
- Testing Isolated Methods
- Test to Production Code Dependencies
- Observing Belonging -> Extract Class Refactoring -> declare a class variable in the old class and make it an instance of the new one -> Move Methods to the New Class -> Review and Reduce the Interfaces -> privatize if possible
- Inverting Dependency Using an Interface
- Analyzing Concerns -> moving methods -> moving tests
- Dissecting Long Methods with Extractions

-------------


Notes and links:
https://www.evernote.com/shard/s84/sh/ab918003-cc8a-426d-bee9-147639882b0f/c7b00fe412f2abe19ee31ab59fa1e929

Screencasts
http://blog.adrianbolboaca.ro/category/code-cast/
