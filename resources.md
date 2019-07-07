---
layout: default
title: Learning Resources
social-description: A list of books, websites, and other useful information for anyone wishing to learn software development
---

Here are a few of the many resources I've used to improve myself and my development skills.  I hope you find these as helpful in your career as I have in mine.

Many of the beginner resources I used when I first started learning to program are books that are no longer in print, so the list below has no true beginner resources.  There are a number of online introductory programming classes, but I didn't start with them, so I can't make informed recommendations for starting points.



## Software Development in General

**Code Complete**<br>
*Author: Steve McConnell / ISBN: 978-0-7356-1967-8*<br>
This should be on every developer's required reading list.  Good practices of software construction are essential to quality maintainable code. This book provides a great foundation for considering implications of decisions early on in the design process, using comments appropriately, and many other topics from large-scale design to small implementation details.

**Udacity [Design of Computer Programs](https://www.udacity.com/course/design-of-computer-programs--cs212)**<br>
*Instructor: Peter Norvig*<br>
To me, this course felt like a light version of SICP, but with fewer parenthesis.  I'd been programming for over a decade when I took this course, so for me, much of its content was as much about learning to write Python in a Pythonic way as it was to design software in general (though it would be good for the latter for anyone not already familiar with software design). 


## SQL

Never underestimate the power of well-written SQL.  Knowing how to get the most out of SQL can be the difference between a query that returns in minutes and one that retuns in fractions of a second.  I listed the books below in the order I read them - the concepts from these books get progressively more advanced, and the advanced books will make more sense if you have the knowledge foundation from the first books.

**Inside SQL Server 2008 T-SQL Querying**<br>
*Authors: Itzik Ben-Gan, Lubor Kollar, Dejan Sarka, Steve Kass / ISBN: 978-0-7356-2603-4*<br>
There is a newer edition currently available, but I used the 2008 edition.  From what I've heard, the the new edition of the book should be as good as the one I read.

**Inside SQL Server 2008 T-SQL Programming**<br>
*Authors: Itzik Ben-Gan, Dejan Sarka, Roger Wolter, Greg Low, Ed Katibah, Isaac Kunen / ISBN: 978-0-7356-2602-7*<br>
Unfortunately, this doesn't appear to be in print any longer, but you can still find e-book editions.  If anyone knows of a more recent book or resource that covers this same material in similar depth, please let me know. 

**Microsoft SQL Server 2012 High-Performance T-SQL Using Window Functions**<br>
*Author: Itzik Ben-Gan / ISBN: 978-0-7356-5836-3*

**Microsoft SQL Server 2014 Query Tuning & Optimization**<br>
*Author: Benjamin Nevarez / ISBN 978-0-07-182942-7*



## Algorithms and Data Structures

**Algorithms 4th Edition**<br>
*Authors: Robert Sedgwick, Kevin Wayne / ISBN: 978-0-321-57351-3*<br>
This book has good detailed implementations of algorithms in Java. When I began reading this, I was working almost exclusively in C#.  The differences between C# and Java are small enough that it was trivially easy for me to make the leap from the book's examples in Java to code I could use in C#.

**[Algorithms Illuminated](http://www.algorithmsilluminated.org/)**<br>
*Author: Tim Roughgarden*<br>
The two books currently available cover about 1/2 of the Coursera specialization listed below.  For me personally, these books instantly just made sense; everything just "clicked" as I was reading them. *Note: the design and implementation of common data structures like linked lists, stacks and queues aren't covered in these books, but you will need to use stacks and queues for graph searches in book 2.*

**Coursera [Algorithms](https://www.coursera.org/specializations/algorithms) specialization**<br>
*Instructor: Tim Roughgarden*<br>
Combined with the books by the same author, any details that were rough after I read the books were filled in by the videos in this specialization.  I thoroughly enjoyed these courses. One of the excercises for one course was the first time I've had to re-write functions that worked with small problems due to a stack overflow with the excercise's large test problem (my code didn't have any infinite loops, the excercise just pushed the limits of recursion that hard).

**Introduction to Algorithms**<br>
*Authors: Cormen, Leiserson, Rivest, Stein / ISBN: 978-0-262-03384-8*<br>
Sometimes referred to as "CLRS", this is considered to be one of the classic texts on the subject.  This was the most recent of my algorithms textbook purchases, and I've used it to improve my knowledge / fill in gaps from the other materials I used for self-study.  This has relatively terse explanations and pseudocode examples.  I find it great for quickly refreshing my memory on an algorithm, but if you're the type that needs working code examples, the other resources I've listed may be more helpful for you.
