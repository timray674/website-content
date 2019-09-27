---
title: 'Links used to activate JavaScript functions'
date: 2019-09-21T07:00:00+02:00
description: 'Which "href" value should I use for JavaScript links, "#" or "javascript:void(0)"?'
tags: js
---

When you are creating an app using plain JavaScript, sometimes you'll have the necessity of triggering a function when the user clicks a link.

You can commonly do this in 2 ways.

Suppose the function you want to execute is called `handleClick()`:

```js
function handleClick() {
  alert('clicked')
}
```

The first way is to use a link like this:

```html
<a href="#" onclick="handleClick()">Click here</a>
```

The second way is to use

```html
<a href="javascript:void(0)" onclick="handleClick()">Click here</a>
```

They are both very similar syntaxes, the only difference is the `href` attribute value.

The first is `href="#"`, the second is `href="javascript:void(0)"`.
You might also see this syntax  `href="javascript:;"`, which is equivalent to the second.

Now, what is the difference in the behavior of those 2 methods?

When the user clicks the `href="#"` link, you *must* make sure that you return `false` from the event handler, the otherwise the browser scrolls back to the top of the page:

```js
function handleClick() {
  alert('clicked')
  return false
}
```

Also, even if you add this but JavaScript is disabled or does not execute for some reason, the browser scrolls back to the top of the page. This is almost always a thing to avoid, so I would personally use the second form, `href="javascript:void(0)"`.

In both ways the `handleClick()` function would not be called if JavaScript is disabled, or there is an error in the JavaScript and so JavaScript execution is halted.

To prevent this, you can use a real URL in the `href` as a fallback, so browsers will move the user to a specific page, using the GET HTTP method, although this is not always possible or convenient.

But it's a best practice and best practices are not always convenient, but you have to factor them in during the design phase of your application, because you can't just build for the ideal use case and ignore all the possible things that could go wrong.

If something goes wrong, the user will blame you and your broken links 🙂