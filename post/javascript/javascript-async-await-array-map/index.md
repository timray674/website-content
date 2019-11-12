---
title: "How to use Async and Await with Array.prototype.map()"
description: "Using async/await combined with map() can be a little tricky. Find out how."
date: 2018-10-11T07:00:00+02:00
updated: 2019-11-04T07:00:00+02:00
tags: js
tags_weight: 29
---

You want to execute an async function inside a `map()` call, to perform an operation on every element of the array, and get the results back.

How can you do so?

This is the correct syntax:

```js
const list = [1, 2, 3, 4, 5] //...an array filled with values

const functionWithPromise = item => { //a function that returns a promise
  return Promise.resolve('ok')
}

const anAsyncFunction = async item => {
  return functionWithPromise(item)
}

const getData = async () => {
  return Promise.all(list.map(item => anAsyncFunction(item)))
}

getData().then(data => {
  console.log(data)
})
```

The main thing to notice is the use of `Promise.all()`, which resolves when all its promises are resolved.

`list.map()` returns a list of promises, so in `result` we'll get the value when everything we ran is resolved.

Remember, we must wrap any code that calls `await` in an `async` function.

See the [promises article](/javascript-promises/) for more on promises, and the [async/await guide](/javascript-async-await/).