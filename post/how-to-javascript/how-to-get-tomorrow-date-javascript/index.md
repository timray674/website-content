---
title: "How to get tomorrow's date using JavaScript"
date: 2019-10-09T07:00:00+02:00
description: "How do you get tomorrow's date using JavaScript?"
tags: js
---

How do you get tomorrow's date using JavaScript?

I had this problem the other day.

So I played a bit with a Date object, in particular with its `getDate()` and `setDate()` methods. The `getDate()` method returns the current day, and `setDate()` method sets the current day.

This is what we're going to do to get tomorrow's date:

1. we first get today's date, using `new Date()`
2. we set a new date by adding `1` to it
3. done!

Using `setDate()` passing the result of `<today>.getDate() + 1`, you'll set the day as "tomorrow".

> If the day is `31` (in months with 31 days) and using `setDate()` you add `1` to the current one, the date will change month and the day will be the first of the new month. Or year, if it's 31 December.

Here's an example:

```js
const today = new Date()
const tomorrow = new Date(today)
tomorrow.setDate(tomorrow.getDate() + 1)
```

`tomorrow` is now a [Date object](/javascript-dates/) representing tomorrow's date. The time did not change - it's still the time you ran the command, increased by 24 hours.

If you also want to reset the time to "tomorrow at 00:00:00", you can do so by calling `tomorrow.setHours(0,0,0,0)`.
