---
title: JavaScript labeled statements
date: 2019-10-23T07:00:00+02:00
description: "A tutorial about a very rarely used JavaScript feature: labeled statements"
tags: js
---

JavaScript has a relatively unknown functionality which allows you to label statements.

I've recently saw this feature used in Svelte to power reactive declarations, which are re-computed whenever the variables declared into the statement change:

```js
$: console.log(variable)
```

They also allow to use a _statement block_, another feature of JavaScript that lets you define a block whenever you can define a statement:

```js
$: {
  console.log(variable)
  console.log('another thing')
  //...
}
```

This may look strange, but it's correct JavaScript. This statement block is assigned to the `$` **label**.

The Svelte compiler internally will use this to power reactive declarations.

I never used this feature anywhere else, yet, but the primary use case is breaking out of a statement that is not the nearest enclosing loop or switch.

Here's a simple example to explain what I mean.

Calling break in any of those points breaks out of the switch, to avoid running the other cases:

```js
for (let y = 0; y < 3; y++) {
  switch (y) {
    case 0:
      console.log(0)
      break
    case 1:
      console.log(1)
      break
    case 2:
      console.log(2)
      break
  }
}
```

This will print `0 1 2` to the console, as expected.

But what if we want to break out of `for` when we reach `case 1`? Here is how:

```js
loop: for (let y = 0; y < 3; y++) {
  switch (y) {
    case 0:
      console.log(0)
      break
    case 1:
      console.log(1)
      break loop
    case 2:
      console.log(2)
      break
  }
}
```

This will print `0 1` to the console.