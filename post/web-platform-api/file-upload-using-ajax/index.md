---
title: How to upload files to the server using JavaScript
description: Uploading a file an process it in the backend in one of the most common file handling functionalities in a web app
date: 2013-10-25T09:07:30+02:00
updated: 2019-10-26T09:07:30+02:00
tags: js
---

Uploading a file and process it in the backend in one of the most common file handling functionalities in a web app: think about uploading an avatar or an attachment.

Say we have an HTML file input element:

```html
<input type="file" id="fileUpload" />
```

We register a change handler on the `#fileUpload` [DOM](/dom/) element, and when the user chooses an image, we trigger the `handleImageUpload()` function passing in the file selected.

```js
const handleImageUpload = event => {
  const files = event.target.files
  const formData = new FormData()
  formData.append('myFile', files[0])

  fetch('/saveImage', {
    method: 'POST',
    body: formData
  })
  .then(response => response.json())
  .then(data => {
    console.log(data.path)
  })
  .catch(error => {
    console.error(error)
  })
}

document.querySelector('#fileUpload').addEventListener('change', event => {
  handleImageUpload(event)
})
```

We use the [Fetch API](/fetch-api/) to send the file to the server. When the server returns successfully, it will send us the image path in the `path` property.

With that, we will do what we need to do, like updating the interface with the image.

## Handling the file upload server-side using Node.js

The server part is detailed here below. I'm using [Node.js](/nodejs/) with the [Express](/express/) framework to handle the request.

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

## Check the properties of the files uploaded client-side

If you need to check the filetype or the file size, you can preprocess them in the `handleImageUpload` function, like this:

```js
const handleImageUpload = event => {
  const files = event.target.files
  const myImage = files[0]
  const imageType = /image.*/

  if (!myImage.type.match(imageType)) {
    alert('Sorry, only images are allowed')
    return
  }

  if (myImage.size > (100*1024)) {
    alert('Sorry, the max allowed size for images is 100KB')
    return
  }

  //...
}
```
