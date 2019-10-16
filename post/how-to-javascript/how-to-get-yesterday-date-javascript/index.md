---
title: "How to get yesterday's date using JavaScript"
date: 2019-10-10T07:00:00+02:00
description: "How do you get yesterdays' date using JavaScript?"
tags: js
---

Well, first you get the date at the current time (today), then you subtract a day from it:

```js
const today = new Date()
const yesterday = new Date(today)

yesterday.setDate(yesterday.getDate() - 1)

today.toDateString()
yesterday.toDateString()
```

We use the `setDate()` method on `yesterday`, passing as parameter the current day minus one.

Even if it's day 1 of the month, JavaScript is logical enough and it will point to the last day of the previous month.