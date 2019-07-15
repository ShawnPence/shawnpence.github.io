---
layout: post
title: What's In A Number?
subtitle: SQL Row_Number(), Rank(), and Dense_Rank()
social-title: What's In A Number? - SQL Row_Number(), Rank(), and Dense_Rank()
social-description: When someone asks for the top N results, make sure to clarify what they really want. SQL's definition may not match that of the person making the request.
css-files:
 - "/css/code.css"
---

Asking questions for clarification is an important developer skill. I've received many requests for the top n records for some criteria. Often times, the request is not intended to return the first n rows (as SQL would return when asked for TOP N in a SELECT statement), but some other variation of rank or dense rank. It is important to understand what is actually needed rather than taking the request at face value.  How are ties to be broken? If there are ties, is numbering of the rank contiguous or are numbers skipped to indicate the relative positions in the data set?

In SQL, ROW_NUMBER(), RANK(), and DENSE_RANK() all provide a way to number records, but each has a different way of dealing with ties. Below are explanations of the functions and examples of how they would apply to the same data with a SQL query. Note: for this blog post, I'm numbering all returned records without partitioning - there's a lot that can be done using partitioning, but that will be a topic for another day.

## The functions

**ROW_NUMBER()** numbers each row in the order it appears (based on the ORDER BY clause). ROW_NUMBER continues numbering without respect for ties.

**RANK()** numbers ties with the same number, but skips sequential numbers according to the number of tied records, then begins the next record after the tie with the same number the row would have received from ROW_NUMBER.

**DENSE_RANK()** numbers ties with the same number, but will continue with the next number in sequence for the next element not part of the current tie.

## Sample Data

Here is a simple example of a Team_Points table with team name and points scored:

| Team | Points |
| - | -: |
| Bears | 7 |
| Cows | 5 |
| Dragons | 7 |
| Elephants | 7 |
| Horses | 4 |
| Lions | 10 |
| Turtles | 5 |
| Wolves | 8 |

## SQL Query / Results

Using the following SQL Query

{% highlight sql %}
  
SELECT
    Team,
    Points,
    ROW_NUMBER() OVER (ORDER BY Points DESC) AS 'Row_Number_',
    RANK() OVER (ORDER BY Points DESC) AS 'Rank_',
    DENSE_RANK() OVER (ORDER BY Points DESC) AS 'Dense_Rank_'
FROM
    Team_Points
ORDER BY
    Points DESC
  
{% endhighlight %}

The results would be as follows:

| Team | Points | Row_Number_ | Rank_ | Dense_Rank_ |
| :- | -: | -: | -: | -: |
| Lions | 10 | 1 | 1 | 1 |
| Wolves | 8 | 2 | 2 | 2 |
| Bears | 7 | 3 | 3 | 3 |
| Dragons | 7 | 4 | 3 | 3 |
| Elephants | 7 | 5 | 3 | 3 |
| Cows | 5 | 6 | 6 | 4 |
| Turtles | 5 | 7 | 6 | 4 |
| Horses | 4 | 8 | 8 | 5 |

 It is important to note that in this query, the order of the teams with the same score is not guaranteed to be deterministic - they may appear in a different order depending on the database system and the order the records were inserted or how they are stored and retrieved by the database engine. Anyone requesting to ignore ties must understand that the results of using ROW_NUMBER() without some form of tiebreaker may not give the expected results.

A SQL Query that includes TOP N after the SELECT statement will return results ending with the row with the same Row_Number() as N. The is a source of confusion when someone unaware of how SQL works asks for the top n results while expecting either RANK() or DENSE_RANK().

<span class="smaller-text"><em>Note: I added an underscore to the end of the aliases used in the query above to avoid having results that use functions as column names. Using keywords, function names, etc. as aliases in SQL can have unintended consequences - that's a post for another day, but please, don't name fields or aliases the same as keywords.</em></span>

## Final Thoughts

The person making a request for ordered results may have a different definition of "top" than what a SQL developer may expect. It is also entirely possible that the person asking for data hasn't even considered the possibility of ties or how they should be handled. It is vital to clarify how ties are to be handled in order to return the data that is needed in the correct format.

*A plea to interviewers or other sample problem writers: If asking for the "Top N" results, please make sure that either the question is worded clearly or that the examples are clear enough to infer which of these methods will give the expected answer. Programmers shouldn't have to resort to guess-and-check due to a poorly worded question.*
