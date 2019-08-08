---
layout: post
title: N<sup>th</sup> Day Of Week in Month Using C#
meta-title: Nth Day Of Week in Month Using C#
social-title: Nth Day Of Week in Month Using C#
social-description: Using C# to find the first Monday in a month (or last Monday, 4th Thursday, etc.)
css-files:
 - "/css/code.css"
---

Events may have a pattern based on day of the week rather than a specific date. For example, the second Tuesday of each month, the last Monday in May, the second Monday in October, etc. The dates for these patterns can be determined programmatically, and this post will show one way to do so using C#.

Below is a code sample in C# followed by an explanation and three example calculations.

[Code Sample](#Code)<br>
[Explanation](#Explanation)<br>
[Example 1](#Example-1) - First Monday in September 2019<br>
[Example 2](#Example-2) - Last Monday in May 2019<br>
[Example 3](#Example-3) - Fourth Thursday in November 2019

## Code

Notes:

- The method below is designed for C#, where days of the week are numbered from 0 to 6 for Sunday through Saturday in the [DayOfWeek](https://docs.microsoft.com/en-us/dotnet/api/system.dayofweek?view=netcore-2.2) enum. Programming languages that use other numbering systems for the days of the week would need alterations to this method or a different method entirely.
- I've seen and used other variations of DayOfWeek math used to achieve the same results. The other variations would replace or alter one or more steps, or use different methods for finding last vs first. I find this method to be the easiest to teach and to understand why it works and visualize on a calendar how it works.

{% highlight csharp %}
 
/// <summary>
/// Find the Nth DayOfWeek in a specified month and year
/// </summary>
/// <param name="n">1 = first or last, 2 = second/next to last, etc.</param>
/// <param name="fromBeginning">True for first, second, etc. 
/// or False for last, next to last.</param>
static DateTime nthDay(int year, int month, int n, DayOfWeek dayOfWeek, bool fromBeginning = true)
{
    //Step 1: the last possible day of month that fits the pattern
    int lastDay;
    if (fromBeginning)
    {
        lastDay = 7 * n;
    }
    else
    {
        //find the last day of the month, then subtract
        lastDay = new DateTime(year, month, 1).AddMonths(1).AddDays(-1).Day - (7 * (n - 1));
    }

    //Step 2: Day of month for Sunday of the week when 
    //          dayOfWeek is the latest possible
    var sundayDayOfMonth = lastDay - (int)dayOfWeek; 

    //Step 3: day of week (0 - 6) in the requested month/year
    //        for the day of month from step 3
    var offset = (int)(new DateTime(year, month, sundayDayOfMonth).DayOfWeek);

    //answer (step 4)
    return new DateTime(year, month, lastDay-offset);

}
 
{% endhighlight %}

## Explanation

### 1. Find the last possible day of the month that could match the rule

This method of date calculation works by subtracting a number representing a day of the week from a specified date. Since this will be subtracting 0 or more days, start with the last possible day that could ever be the n<sup>th</sup> day (e.g. the 7<sup>th</sup> is the last possible day that could be the first Monday).

The last possible day of the month for the n<sup>th</sup> DayOfWeek will always be 7 &times; n. For example, the latest possible day that could be the 1<sup>st</sup> Monday is the 7<sup>th</sup>;  similarly, the last possible day of month for the 4<sup>th</sup> Thursday would be the 28<sup>th</sup>.

If you need the last or n<sup>th</sup> from last instead, use the last day of the month and subtract 7(n-1) from the last day of the month  For example, the lastest date for the next to last Monday in May would be the 24th, or 31 - 7(2-1).

### 2. Find the day of the month for Sunday of the week when the specified day of week is on the last day possible (from step 1)

Why Sunday? In C#, Sunday is 0 in the [DayOfWeek](https://docs.microsoft.com/en-us/dotnet/api/system.dayofweek?view=netcore-2.2) enum. To figure out the correct day in a specific year, this method subtracts days from the last possible day that could possibly meet the criteria. As the day of the month calculated from step 2 moves forward by one day of the week, the n<sup>th</sup> day will be one day of the month earlier. To find Sunday of the week, subract the DayOfWeek requested from the number from step 1.

### 3. Find the day of week of the date from step 2 in the specified year

To know how many days to subtract, determine the day of the week for the requested year, month, and the day of the month from step 2.

### 4. Subtract the day of week (from step 3) from the last possible day (from step 1)

The result from (step 1) - (step 3) is the day of the month.

## Examples

*To avoid the possible confusion between month/day/year and day/month/year systems of dates, I'll list dates using ISO date format of YEAR-MONTH-DAY.*

### Example 1

**Find the first Monday in September 2019**

Step 1:<br>
Multiply n times 7 - in the case of first Monday, n = 1.<br>
7 &times; 1 = **7**

Step 2:<br>
Find Sunday if the specified DayOfWeek is the last possible day of the month that would fit the pattern.<br>
In C# (where Sunday is day 0), Monday is day 1. *If Monday was the 7<sup>th</sup>, Sunday would be the 6<sup>th</sup>*<br>
7 - 1 = **6**

Step 3:<br>
Find the day of week for step 2's day of month in the specified year:<br>
In 2019, September 6th is on Friday, which is **5** in the DayOfWeek enum.

Step 4:<br>
Subtract step 3's answer from step 1
7 - 5 = **2**

The first Monday in September 2019 is the 2<sup>nd</sup> so the date is 2019-09-02.

### Example 2

**Find the last Monday in May 2019**

Step 1:<br>
For LAST, multiply (n - 1) times 7, and subtract from the last day of the month:<br>
The last day of May is the 31st. For last, n = 1 (next to last would be n=2, etc).<br>
31 - (7 &times; (1 - 1)) = **31**

Step 2:<br>
Find Sunday in a week where DayOfWeek is on the last possible day of month that fits the pattern. Since Monday is 1 in DayOfWeek, subtract 1. *If Monday was the 31<sup>st</sup>, Sunday would be the 30<sup>th</sup>*<br>
31 - 1 = **30**

Step 3:<br>
Find the day of week for step 2's day of month in the specified year:<br>
In 2019, May 30 is on Thursday, which is **4** in the DayOfWeek enum.

Step 4:<br>
Subtract step 3 from step 1:<br>
31 - 4 = **27**

The last Monday of May 2019 is the 29<sup>th</sup> so the date is 2019-05-27.

### Example 3

**Find the fourth Thursday in November 2019**

Step 1:<br>
Multiply n times 7 - in the case of fourth Thursday, n = 4.
4 &times; 7 = **28**

Step 2:<br>
Find Sunday in a week where DayOfWeek is on the last possible day of month that fits the pattern.<br>
Since Thursday is 4 in DayOfWeek, subtract 4. *If Thursday is the 28<sup>th</sup>, Sunday of the same week would be the 24<sup>th</sup>*<br>
28 - 4 = **24**

Step 3:<br>
Find the day of week for step 2's day of month in the specified year:<br>
In 2019, November 24 is on Sunday, which is **0** in the DayOfWeek enum.

Step 4:<br>
Subtract step 3 from step 1:<br>
28 - 0 = **28**

The fourth Thursday of November 2019 is the 28<sup>th</sup> so the date is 2019-11-28.