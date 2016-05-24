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

[Php Source code](https://github.com/peter-wilkins-mayden/solid-foundation). Instructions are in the commit messages so run ```git log``` to see them but you probably need to watch the talk to understand. Below are the scrambled notes I took:

Single Responsibility
---
The printer() function gives us good encapsulation, but the report class violates Single Responsibility. why? because there are 3 reasons to change, a new format, different data source or different printer.
    Refactor to classes with Single Responsibilities....

 >make more classes, (measure no of classes, average class size in iaptus) why? clarity, boundaries, make change without risk of breaking other functionality, change != merge conflicts (class diagram tool)

>Intro code, printer() = good encap, violates SR, why? 3 reasons to change, refactor, commit
much more complicated? much safer and clearer, why? possible to not touch code unless you have to now. merge conflicts?

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

>don't change a class, extend it. repeat up the call graph to the 'polymorphic switch'. Make common functionality final.
why? don't lose flexibility when adding capability, change != merge conflicts.

>Add 11x17, don't break OC, change it back (no reverts, conflicts etc), write command arg - bonus.
Printers are broken - wrong printer, new printer,

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

>good naming helps here:  $report = new TabloidReport() (<-spoc)  	abstract : concrete    (no. of substitutable initializations)
Is Report a good name? just as specialized as TabloidReport, rename it.
$letterReport = new TabloidReport() , just wrong, LS violation, why naming matters so much.
why? lets change the report type - simples

Interface Segregation
---
If you look you will see DataAccess implements an Interface, but does
not implement most of the functions as it does not need to. this is a
problem as another class may call these functions and break our program.

There may be other classes using IDataAccess we cannot touch it.
Instead create 3 new interfaces called IGetData, IPersistData and IDeleteData
and split out the functions.

Now we can get rid of the problem functions in DataAccess.

>(interface small) don't make clients do work they do not need to.   (no of interfaces, average size)
API decomposition (break interfaces down) then recompose using TooBigInterface extends goodInterface to maintain BC (possible in php?)
naming: behaviours not things - IGetData, IQueryData, IPersistData
why? now easier to add functions and add to obvious interface, consume like behaviors as a unit.

Inversion of Dependencies
----
These report classes are deciding to much, such as which printer to use.  They are Micro-managers. Instead, we want to make these decisions so lets pass the dependencies into the constructor.

Go to it!

>high classes know 'what but not how', low classes only know how to do their (tiny) part of system
don't create objects in class (micro managers), pass objects into the constructor (<-spoc)   (measure no of new()'s outside of controllers)
when you remove the low level details from a high class, your code can now be dryer, but there
a sweet spot for flexibility where too flexible brings as much risk as being too rigid.
 Create stupid classes that don't know the specifics of how to do things but know how to use low level classes to  complete tasks at a higher abstraction.

Now we  have type hints in the constructor, we are safe from sending the wrong size report to the wrong printer.

As a final exercise, take a look at TabloidReport and LetterReport, switch back and forth quickly.
   I hope you noticed they are very identical part from the type hints.
   Dry the code by removing TabloidReport and LetterReport.
   Make the type hints more general in Program. Yay polymorphism.
   What are the advantages and disadvantages? What do you prefer?

Conclusion.
---
>Decide how far to take decomposition. ROI?: greater flexibility vs the extra work to (re) compose
Someone’s 'Cutting corners' is another’s 'valid ROI call'.
Thinking long term, there is more cost to 'just get it done' if others have to come back and fix the work.
