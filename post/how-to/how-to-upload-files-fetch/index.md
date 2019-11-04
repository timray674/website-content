---
title: How to upload a file using Fetch
description: How to upload files to the server using the Fetch API, explained in a simple way
date: 2019-10-30T07:00:00+02:00
tags: js
---

There's a task that should be simple, but sometimes it leads to hours of research on the Web: uploading files to the server.

In this tutorial I explain you how to do so using [`fetch`](/fetch-api/).

Given a form with a file input field:

```html
<input type="file" id="fileUpload" />
```

We attach a `change` event handler on it:

```js
document.querySelector('#fileUpload').addEventListener('change', event => {
  handleImageUpload(event)
})
```

and we manage the bulk of our logic in the `handleImageUpload()` function:

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
    console.log(data)
  })
  .catch(error => {
    console.error(error)
  })
}
```

In this example we POST to the `/saveImage` endpoint.

We initialize a new `FormData` object and we assign it to the `formData` variable, and we append there the uploaded file. If we have more than one file input element, we'd have more than one `append()` call.

The `data` variable inside the second `then()` will contain the JSON parsed return data. I'm assuming your server will give you JSON as a response.

How to handle images uploaded server-side is a different topic, one I'll write about tomorrow.
