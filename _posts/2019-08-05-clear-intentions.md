---
layout: post
title: Make Your Intentions Clear
social-title: Make Your Intentions Clear
social-description: When writing code, don't rely on order of operations - make the intent of your code clear.
css-files:
 - "/css/code.css"
---
It seems that every few weeks I see another argument online over a viral math problem. Inevitably, the problem will involve parenthesis placed for the purpose of causing confusion instead of adding clarity. While I usually enjoy math puzzles, I’ve never cared for trick questions that rely on intentionally poorly-written problems where the puzzle is not a challenge to be solved, but is instead, a lack of clarity on the part of the person writing the problem. These lead to incorrect answers based not on the reader’s math skill, but based on the problem writer’s (often intentional) failure to write a clear question.

This issue is not, however, unique to math problems. I’ve more than once debugged someone else’s code only to find that the error they were encountering was caused by incorrect assumptions about the order of operations with logical AND and OR operators. In many programming languages (including the two I use most often, C# and SQL), AND has a higher priority than OR. If a developer fails to make their intentions clear with parenthesis and fails to consider the order of operations, they can get unexpected results.

For example, take a SQL query looking for a car that seats at least 6 people and is either red or blue. I’ve come across code samples like the one below that don’t work as the person writing the query expected.

**Incorrect:**

{% highlight sql %}
 
SELECT * FROM cars WHERE color = 'red' OR color = 'blue' AND seats >= 6
 
{% endhighlight %}

The query above will return all cars that are red (regardless of the number of seats) or cars that are both blue and seat 6 or more people. The order of operations will yield results that are the same as the following query.

**Incorrect *(with parenthesis added to show how the implied order of operations will evaluate the query)*:**

{% highlight sql %}
 
SELECT * FROM cars WHERE color = 'red' OR (color = 'blue' AND seats >= 6)
 
{% endhighlight %}

Instead of relying on order of operations, always use parenthesis to make intent clear.

**Correct:**

{% highlight sql %}
 
SELECT * FROM cars WHERE (color = 'red' OR color = 'blue') AND seats >= 6
 
{% endhighlight %}

While the examples above are simple and easy to understand, I’ve come across bugs that took significantly more time to uncover that were buried in WHERE clauses dozens of lines long or in nested subqueries. Writing clear code the first time is much easier to deal with than trying to dig through someone else’s code and determine their intent.

Even if the order of operations for multiple AND and OR statements would already yield the correct results, adding parenthesis can help future developers know your intent and ensure that modifications to the code don’t cause unexpected side effects. Clear code leads to fewer bugs and less time spent debugging. The few extra keystrokes used to add parenthesis can save significant pain down the road when others have to debug, extend, or refactor the code. Always strive to make the intent of the code clear rather than relying on operator precedence.
