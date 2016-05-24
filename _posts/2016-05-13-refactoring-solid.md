---
title: "Refactoring to a S.O.L.I.D. Foundation, Steve Bohlen"
layout: post
date: 2016-02-25 22:44
blog: true
star: true
---
Refactoring to a S.O.L.I.D. Foundation, Steve Bohlen
--
[Steve Bohlen's excellent talk](https://www.youtube.com/watch?v=huEEkx5P5Hs&ab_channel=ExcellaConsulting) really helped me understand and put into practise the solid principles so I ported the exercise to PHP.

[Php Source code](https://github.com/peter-wilkins-mayden/solid-foundation). The is one commit per section below. Instructions are also in the commit messages.

Single Responsibility
---
The printer() function gives us good encapsulation, but the report class violates Single Responsibility. why? because there are 3 reasons to change, a new format, different data source or different printer.
    Refactor to classes with Single Responsibilities....

 >Why make more classes? for clarity, boundaries, the ability to make change without risk of breaking other functionality, fewer merge conflicts


Open Closed
---
 Why have we made the program much more complicated?  It is now much safer and clearer, why? because we made it possible to not touch code unless you have to. Not to mention less merge conflicts!

 Now the Boss wants bigger reports! He wants 11x17.
 Refactor the code to add the new feature but don't break the Open Closed Principle!
Don't touch ReportFormatter (hint: use inheritance)
Oh, don't touch Report either!

and now the printers are backed up - only the dot matrix printer can
print 11x17
fix it!

>Why extend a class instaed of changing it? don't lose flexibility when adding capability, easy to revert, fewer merge conflicts, can lead to polymorphism.

Liskoff Substitution
---
Names are a great help with Liskof Substition
$report = new TabloidReport() makes sense however the Report classes name is now too vague.
Make it better.

There are two more classes that need renaming... do that.

Now that we have renamed the classes have a think about what is now missing.

What would Barbara do?

Also, check that all your derived types (on the right of the =) have
more specific names than the names on the left.


Use derived types (polymorphism) .... without knowing it.
No polymorphic checks: if($thisConcreteClass){...} elseif(thatConcreteClass){...}  violation!

>Good naming helps here:
$report = new TabloidReport()  	abstract type on left, concrete type on the right


Interface Segregation
---
If you look you will see DataAccess implements an Interface, but does
not implement most of the functions as it does not need to. this is a
problem as another class may call these functions and break our program.

There may be other classes using IDataAccess we cannot touch it.
Instead create 3 new interfaces called IGetData, IPersistData and IDeleteData
and split out the functions.

Now we can get rid of the problem functions in DataAccess.

>Don't make clients do work they do not need to.
naming: behaviours not things - IGetData, IQueryData, IPersistData
Why? adds clarity to the interfaces purpose

Inversion of Dependencies
----
These report classes are deciding to much, such as which printer to use.  They are Micro-managers. Instead, we want to make these decisions so lets pass the dependencies into the constructor.

Go to it!

>High level classes know 'what but not how', low level classes only know how to do their one responsibility.
 Don't create objects in class, pass objects into the constructor.


Now we  have type hints in the constructor, we are safe from sending the wrong size report to the wrong printer.

Conclusion.
---
As a final exercise, take a look at TabloidReport and LetterReport.
   I hope you noticed they are almost identical apart from the type hints.
   Dry the code by removing TabloidReport and LetterReport.
   Make the type hints more general in Program. Yay polymorphism.
   What are the advantages and disadvantages? What do you prefer?


>Decide how far to take decomposition. ROI?: greater flexibility vs the extra work to (re) compose
Someone’s 'Cutting corners' is another’s 'valid ROI call'.
Thinking long term, there is more cost to 'just get it done' if others have to come back and fix the work.
