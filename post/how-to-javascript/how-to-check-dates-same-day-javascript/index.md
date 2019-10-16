---
title: "How to check if two dates are the same day in JavaScript"
date: 2019-10-12T07:00:00+02:00
description: "How do you detect if a date object instance in JavaScript refers to the same day of another date object?"
tags: js
---

How do you detect if a date object instance in JavaScript refers to the same day of another date object?

JavaScript does not provide this functionality in its standard library, but you can implement it using the methods

- `getDate()` returns the day
- `getMonth()` returns the month
- `getFullYear()` returns the 4-digits year

This is a simple function you can copy/paste to do the check:

```js
const datesAreOnSameDay = (first, second) =>
    first.getFullYear() === second.getFullYear() &&
    first.getMonth() === second.getMonth() &&
    first.getDate() === second.getDate();
```

Example usage:

```js
datesAreOnSameDay(new Date(), new Date()) //true
```