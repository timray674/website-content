---
title: How to get the days between 2 dates in JavaScript
date: 2019-10-26T07:00:00+02:00
description: "Given two JavaScript `Date` objects, how can I get a list of the days (expressed as Date objects, too) between those 2 dates?"
tags: js
---

I had this problem: given two JavaScript `Date` objects, how can I get a list of the days (expressed as Date objects, too) between those 2 dates?

Here's a function to calculate that.

It gets 2 date objects as parameters, and returns an array of Date objects:

```js
const getDatesBetweenDates = (startDate, endDate) => {
  let dates = []
  //to avoid modifying the original date
  const theDate = new Date(startDate)
  while (theDate < endDate) {
    dates = [...dates, new Date(theDate)]
    theDate.setDate(theDate.getDate() + 1)
  }
  return dates
}
```

Example usage:

```js
const today = new Date()
const threedaysFromNow = new Date(today)
threedaysFromNow.setDate( threedaysFromNow.getDate() + 3)

getDatesBetweenDates(today, threedaysFromNow)
```

If you also want to include the start and end dates, you can use this version that adds it at the end:

```js
const getDatesBetweenDates = (startDate, endDate) => {
  let dates = []
  //to avoid modifying the original date
  const theDate = new Date(startDate)
  while (theDate < endDate) {
    dates = [...dates, new Date(theDate)]
    theDate.setDate(theDate.getDate() + 1)
  }
  dates = [...dates, endDate]
  return dates
}
```