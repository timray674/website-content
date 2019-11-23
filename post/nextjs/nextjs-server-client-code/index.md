---
title: "Next.js: run code only on the server side or client side"
description: "How to write code that's only executed on one side of your stack: frontend or backend"
date: 2019-11-21T07:00:00+02:00
tags: next
---

In your page components, you can execute code only in the server-side or on the client-side, but checking the `window` property.

This property is only existing inside the browser, so you can check

```js
if (typeof window === 'undefined') {

}
```

and add the server-side code in that block.

Similarly, you can execute client-side code only by checking

```js
if (typeof window !== 'undefined') {

}
```

> JS Tip: We use the `typeof` operator here because we can't detect a value to be undefined in other ways. We can't do `if (window === undefined)` because we'd get a "window is not defined" runtime error

Next.js, as a build-time optimization, also removes the code that uses those checks from bundles. A client-side bundle will not include the content wrapped into a `if (typeof window === 'undefined') {}` block.