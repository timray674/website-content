---
title: "How to use the Next.js Router"
description: "Learn how to use the `next/router` package to control routes in Next.js"
date: 2019-11-28T07:00:00+02:00
tags: next
---

We already saw how to use the Link component to declaratively handle routing in Next.js apps.

It's really handy to manage routing in JSX, but sometimes you need to trigger a routing change programatically.

In this case, you can access the Next.js Router directly, provided in the `next/router` package, and call its `push()` method.

Here's an example of accessing the router:

```js
import { useRouter } from 'next/router'

export default () => {
  const router = useRouter()
  //...
}
```

Once we get the router object by invoking `useRouter()`, we can use its methods.

> This is the client side router, so methods should only be used in frontend facing code. The easiest way to ensure this is to wrap calls in the `useEffect()` React hook, or inside `componendDidMount()` in React stateful components.

The ones you'll likely use the most are `push()` and `prefetch()`.

`push()` allows us to programmatically trigger a URL change, in the frontend:

```js
router.push('/login')
```

`prefetch()` allows us to programmatically prefetch a URL, useful when we don't have a `Link` tag which automatically handles prefetching for us:

```js
router.prefetch('/login')
```

Full example:

```js
import { useRouter } from 'next/router'

export default () => {
  const router = useRouter()

  useEffect(() => {
    router.prefetch('/login')
  })
}
```

You can also use the router to listen for [route change events](https://nextjs.org/docs#router-events).