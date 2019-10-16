---
title: "How to get the month name from a JavaScript date"
date: 2019-10-11T07:00:00+02:00
description: "Given a JavaScript Date object instance, how can you get a string that represents the month name?"
tags: js
---

Given a JavaScript Date object instance, how can you get a string that represents the month name?

In other words, from

```js
const today = new Date()
```

how can we get the **month name**?

Every Date object instance has a `toLocaleString()` method, which is one of the [JavaScript internationalization methods](/javascript-internationalization/).

Using it you can get the month name in your current locale, and here's how you can use it:

```js
const today = new Date()
today.toLocaleString('default', { month: 'long' })
```

Depending on your current locale you'll get a different result. I get "October" as a result.

Using the `short` format for the date, I get "Oct":

```js
today.toLocaleString('default', { month: 'short' })
```

The first parameter, to which we pass the `default` string, is the locale. You can pass any locale you want, for example `it-IT` will return you `ottobre`:

```js
const today = new Date()
today.toLocaleString('it-IT', { month: 'long' })
```
