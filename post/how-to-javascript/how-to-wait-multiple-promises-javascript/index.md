---
title: How to wait for 2 or more promises to resolve in JavaScript
date: 2019-10-25T07:00:00+02:00
description: "Say you need to fire up 2 or more promises and wait for their result. How to do that?"
tags: js
---

Say you need to fire up 2 or more [promises](/javascript-promises/) and wait for their result.

And you want to go on, once you have both resolved.

How can you do so, in JavaScript?

You use `Promise.all()`:

```js
const promise1 = //...
const promise2 = //...

const data = await Promise.all([promise1, promise2])

const dataFromPromise1 = data[0]
const dataFromPromise2 = data[1]
```

If you prefer using pure promises and not [async/await](/javascript-async-await/), use this syntax:

```js
const promise1 = //...
const promise2 = //...

Promise.all([promise1, promise2]).then(data => {
	const dataFromPromise1 = data[0]
	const dataFromPromise2 = data[1]
}
```
