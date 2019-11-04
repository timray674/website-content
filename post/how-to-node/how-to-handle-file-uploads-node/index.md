---
title: How to handle file uploads in Node.js
description: How to use Node.js and in particular Express to handle uploaded files
date: 2019-10-31T07:00:00+02:00
tags: node
---

In [how to upload a file using Fetch](/how-to-upload-files-fetch/) I explained how to upload a file to a server using [Fetch](/fetch-api/).

In this post I'm going to show you part 2: how to use [Node.js](/nodejs/), and in particular [Express](/express/), to handle uploaded files.

Install the [`express-fileupload`](https://www.npmjs.com/package/express-fileupload) npm module:

```sh
npm install express-fileupload
```

and add it to your middleware:

```js
import fileupload from 'express-fileupload'

//or

const fileupload = require('express-fileupload')
```

After you created your Express app, add:

```js
app.use(
  fileupload(),
  //...
```

This is needed because otherwise the server can't parse file uploads.

Now uploaded files are provided in `req.files`. If you forget to add that middleware, `req.files` would be `undefined`.

```js
app.post('/saveImage', (req, res) => {
  const fileName = req.files.myFile.name
  const path = __dirname + '/images/' + fileName

  image.mv(path, (error) => {
    if (error) {
      console.error(error)
      res.writeHead(500, {
        'Content-Type': 'application/json'
      })
      res.end(JSON.stringify({ status: 'error', message: error }))
      return
    }

    res.writeHead(200, {
      'Content-Type': 'application/json'
    })
    res.end(JSON.stringify({ status: 'success', path: '/img/houses/' + fileName }))
  })
})
```

This is the smallest amount of code needed to handle files.

We call the `mv` property of the uploaded image. That is provided to us by the `express-fileupload` module. We move it to `path` and then we communicate the success (or an error!) back to the client.
