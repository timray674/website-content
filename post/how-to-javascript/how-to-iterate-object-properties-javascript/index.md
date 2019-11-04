---
title: How to iterate over object properties in JavaScript
description: "Here's a very common task: iterating over an object properties, in JavaScript"
date: 2019-11-02T07:00:00+02:00
tags: js
---

If you have an object, you can't just iterate it using `map()`, `forEach()` or a `for..of` loop.

You will get errors:

```js
const items = {
  'first': new Date(),
  'second': 2,
  'third': 'test'
}
```

`map()` will give you `TypeError: items.map is not a function`:

```js
items.map(item => {})
```

`forEach()` will give you `TypeError: items.forEach is not a function`:

```js
items.forEach(item => {})
```

`for..of` will give you `TypeError: items is not iterable`:

```js
for (const item of items) {}
```

So, what can you do to iterate?

You can call **`Object.entries()`** to generate an array with all its enumerable properties, and loop through that, using any of the above methods:

```js
Object.entries(items).map(item => {
  console.log(item)
})

Object.entries(items).forEach(item => {
  console.log(item)
})

for (const item of Object.entries(items)) {
  console.log(item)
}
```
