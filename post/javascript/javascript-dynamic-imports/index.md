---
title: "JavaScript Dynamic Imports"
description: "Learn this new, upcoming feature of JavaScript"
date: 2019-11-08T07:00:00+02:00
tags: js
---

I have never had the privilege to use **dynamic imports** until very recently when I used them to power code splitting in a Next.js application, and I had to do a bit of research because they are slightly different from *static imports*.

A static import of an ES Module *default export* looks like this:

```js
import moment from 'moment'
```

You can use object destructuring to get a named export:

```js
import { format } from 'date-fns'
```

Static imports have some limits:

- they are limited to the top level of the file
- they can't be loaded conditionally (inside an `if`)
- the name of the package can't be determined at execution time

Dynamic imports can do all those things!

The syntax is a little bit different.

And they work _within modules_.

You use them like this:

```js
const module = await import('module')
```

and to use the default export, you must first call `.default()`.

Example using moment:

```js
const moment = (await import('moment')).default()
```

Named imports on the other hand work as expected:

```js
const { format } = await import('date-fns')
```

Can you use them today? Yes! The [browser support](https://caniuse.com/#feat=es6-module-dynamic-import) is already pretty good, and there's also a [Babel plugin](https://babeljs.io/docs/en/babel-plugin-syntax-dynamic-import).

