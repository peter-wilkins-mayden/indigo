---
title: "Refactoring to a S.O.L.I.D. Foundation, Steve Bohlen"
layout: post
date: 2016-02-25 22:44
blog: true
star: true
---
Refactoring to a S.O.L.I.D. Foundation, Steve Bohlen
--
https://www.youtube.com/watch?v=huEEkx5P5Hs&ab_channel=ExcellaConsulting

Php Source code: https://github.com/peter-wilkins-mayden/solid-foundation/

###Single Responsibility:
 make more classes, (measure no of classes, average class size in iaptus) why? clarity, boundaries, make change without risk of breaking other functionality, change != merge conflicts (class diagram tool)

Intro code, printer() = good encap, violates SR, why? 3 reasons to change, refactor, commit
much more complicated? much safer and clearer, why? possible to not touch code unless you have to now. merge conflicts?

###Open Closed:
don't change a class, extend it. repeat up the call graph to the 'polymorphic switch'. Make common functionality final.
why? don't lose flexibility when adding capability, change != merge conflicts.

Add 11x17, don't break OC, change it back (no reverts, conflicts etc), write command arg - bonus.
Printers are broken - wrong printer, new printer,

###Liskoff Substitution:
Use derived types (polymorphism) .... without knowing it.
No polymorphic checks: if($thisConcreteClass){...} elseif(thatConcreteClass){...}  violation!

good naming helps here:  $report = new TabloidReport() (<-spoc)  	abstract : concrete    (no. of substitutable initializations)
Is Report a good name? just as specialized as TabloidReport, rename it.
$letterReport = new TabloidReport() , just wrong, LS violation, why naming matters so much.
why? lets change the report type - simples

###Interface Segregation:
(interface small) don't make clients do work they do not need to.   (no of interfaces, average size)
API decomposition (break interfaces down) then recompose using TooBigInterface extends goodInterface to maintain BC (possible in php?)
naming: behaviours not things - IGetData, IQueryData, IPersistData
why? now easier to add functions and add to obvious interface, consume like behaviors as a unit.

### Inversion of Dependencies:
high classes know 'what but not how', low classes only know how to do their (tiny) part of system
don't create objects in class (micro managers), pass objects into the constructor (<-spoc)   (measure no of new()'s outside of controllers)
when you remove the low level details from a high class, your code can now be dryer, but there
a sweet spot for flexibility where too flexible brings as much risk as being too rigid.
 Create stupid classes that don't know the specifics of how to do things but know how to use low level classes to  complete tasks at a higher abstraction.


###Conclusion.
Decide how far to take decomposition. ROI?: greater flexibility vs the extra work to (re) compose
Someone’s 'Cutting corners' is another’s 'valid ROI call'.
Thinking long term, there is more cost to 'just get it done' if others have to come back and fix the work.
