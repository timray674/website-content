---
title: How to get both parsed body and raw body in Express
description: "Find out how to get both parsed body and raw body in Express with `body-parser`"
date: 2019-10-29T07:00:00+02:00
tags: node
---

In one application I'm building, I had this problem.

Using Express, I can import `body-parser` to parse the body as JSON:

```js
import bodyParser from 'body-parser'
```

```js
app.use(bodyParser.json())
```

However to integrate with the Stripe payments API I had the need to expose the **raw body** (not parsed) into an endpoint, and I couldn't figure out how to do it, while still parsing the body as JSON.

This did the trick:

```js
app.use(bodyParser.json({
  verify: (req, res, buf) => {
    req.rawBody = buf
  }
}))
```

Now the raw body is available on `req.rawBody` and the JSON parsed data is available on `req.body`.

From the `body-parser` GitHub I found that this doubles the RAM usage for every request, but since I need this functionality, I have no other way.

Except perhaps creating a different server just for the Stripe webhook I wanted to handle.