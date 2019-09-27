---
title: How to check if a JavaScript value is an array?
date: 2019-09-25T07:00:00+02:00
description: "Find out how to determine if a JavaScript value is an array using the `Array.isArray()` method"
tags: js
---

Sometimes you got passed an object in a function, and you need to check if this is an array.

Maybe if it's an array you perform some operation, and if it's not an array you perform something else.

How can you determine if an object is an array?

Use the `isArray()` static method provided by the `Array` built-in object, introduced in ECMAScript 5:

```js
const list = [1, 2, 3]
Array.isArray(list) //true
```
