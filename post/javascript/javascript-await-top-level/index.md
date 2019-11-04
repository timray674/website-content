---
title: How to use top-level await in ES Modules
description: "Learn how to use this new feature currently available in v8"
date: 2019-11-05T07:00:00+02:00
tags: js
---

[v8](/v8/) recently introduced top-level `await` for ES modules. It's a new proposed standard for ECMAScript, which has [reached stage 3](https://github.com/tc39/proposal-top-level-await).

> Note: it's going to take some time before this feature will be usable in the production Node.js and in Chrome, but it's worth taking a look

Right now we can use await _only inside async functions_. So it's common to declare an immediately invoked async function expression to wrap it:

```js
(async () => {
  await fetch(/* ... */)
})()
```

or also declare a function and then call it:

```js
const doSomething = async () => {
  await fetch(/* ... */)
}

doSomething()
```

Top-level await will allow us to simply run

```js
await fetch(/* ... */)
```

without all this boilerplate code.

With a caveat: this only works **in ES modules**. You can't use this syntax outside of [ES modules](/how-to-enable-es-modules-nodejs/).

Normal scripts, and CommonJS modules, will continue to use [immediately invoked function expressions](https://flaviocopes.com/javascript-iife/) or creating ad-hoc function like always.