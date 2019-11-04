---
title: How to calculate the number of days between 2 dates in JavaScript
description: "I had this problem: how do I calculate the number of days between 2 dates?"
date: 2019-11-04T07:00:00+02:00
tags: js
---

In particular, I wanted to count the number of nights that a person had to pay to rent a house and sleep in it, depending on the checkin [date](/javascript-dates/), and the checkout date.

I looked at different solutions, and the one that gave me the least problems, considering all the issues with dates (including DST), was this: starting from the starting date, we add one day until the date represents a date after the end date.

Here's the code:

```js
const numberOfNightsBetweenDates = (startDate, endDate) => {
  const start = new Date(startDate) //clone
  const end = new Date(endDate) //clone
  let dayCount = 0

  while (end > start) {
    dayCount++
    start.setDate(start.getDate() + 1)
  }

  return dayCount
}
```

I first clone the dates we are given, because dates are objects, and we get a _reference_ to that object. This means that using `setDate()` in the function would also affect the variable outside of this function - not something we look forward to!

That's it.

If instead you want to get the number of days between 2 dates (say, today to tomorrow is 2 days), just change `while (end > start)` to `while (end >= start)`. That would work. Or increase the `dayCount` starting point to `1`.