---
title: How to join two arrays in JavaScript
date: 2019-09-23T07:00:00+02:00
description: "Find out how to merge two or more arrays using JavaScript"
tags: js
---

Suppose you have two arrays:

```js
const first = ['one', 'two']
const second = ['three', 'four']
```

and you want to merge them into one single array

How can you do so?

The modern way is to use the destructuring operator, to create a brand new array:

```js
const result = [...first, ...second]
```

This is what I recommend. Note that this operator was introduced in ES6, so older browsers (read: Internet Explorer) might not support it.

If you want a solution that works also with older browsers, you could use the `concat()` method which can be called on any array:

```js
const result = first.concat(second)
```

Both methods will generate a new array, without modifying the existing ones.