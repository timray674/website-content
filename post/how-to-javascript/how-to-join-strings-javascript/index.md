---
title: How to join two strings in JavaScript
date: 2019-09-22T07:00:00+02:00
description: "Find out how to combine strings using JavaScript"
tags: js
---

JavaScript, like any good language, has the ability to join 2 (or more, of course) strings.

How?

We can use the `+` operator.

If you have a string `name` and a string `surname`, you can assign those too the `fullname` variable like this:

```js
const fullname = name + surname
```

If you don't want to instantiate a new variable, you can use the `+=` operator to add the second string to the first:

```js
name += surname
```

Alternatively you can also use the `concat()` method of the String object, which returns a new string concatenating the one you call this method on, with the argument of the method:


```js
const fullname = name.concat(surname)
```

I generally recommend the simplest route (which also happen to be the faster) which is using the `+` (or `+=`) operator.