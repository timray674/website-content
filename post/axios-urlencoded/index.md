---
title: "How to send urlencoded data using Axios"
date: 2019-10-04T07:00:00+02:00
description: "Learn how to send urlencoded data using Axios"
tags: js
---

I had this problem: an API I had to call from a Node.js app was only accepting data using the urlencoded format.

I had to figure out this problem: how to send urlencoded data using Axios?

The first thing we need to do is to install the [`qs`](https://www.npmjs.com/package/qs) module. It's a cool querystring parsing and stringifying library with some added security:

```sh
npm install qs
```

Then we need to import the `qs` module along with the Axios import, of course:

```js
const qs = require('qs')
const axios = require('axios')
```

If you use ES Modules, use

```js
import qs from 'qs'
import axios from 'axios'
```

Next, the Axios code. Check my full [Axios tutorial](/axios/) if you are not familiar with it.

In short, we need to use the full form for the Axios request. Not `axios.post()` but `axios()`.

Inside there, we use the `stringify()` method provided by `qs` and we wrap the data into it. We then set the `content-type` header:

```js
axios({
  method: 'post',
  url: 'https://my-api.com',
  data: qs.stringify({
    item1: 'value1',
    item2: 'value2'
  }),
  headers: {
    'content-type': 'application/x-www-form-urlencoded;charset=utf-8'
  }
})
```