---
title: How to add comments in Svelte templates
date: 2019-10-08T07:00:00+02:00
description: "How to avoid Svelte to render parts of a template to the client"
tags: svelte
---

HTML comments are great to hide elements from a page.

In HTML here's how you add a comment:

```html
<!-- a comment here -->
```

You can use this on blocks, too, to hide multiple lines of HTML:

```html
<!--
a
 comment
  here
-->
```

Note that this is still visible in the page source. The browser just hides it, but one can always go and see the comment.

You can use the same comments in your Svelte templates. But with Svelte you don't send the commented part to the browser. That part is completely removed, and only stay in your source files, invisible to the HTML generated into the page.

Which in my opinion is a positive thing.