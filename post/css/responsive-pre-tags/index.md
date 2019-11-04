---
title: Responsive pre tags in CSS
date: 2019-10-27T07:00:00+02:00
description: "I've had some problems with responsiveness in a few posts, on my blog. Turned out it was code snippets"
tags: js
---

I've had some problems with responsiveness in a few posts, on my blog.

Turns out those posts I had problems on, they all had a snippet of code that went beyond the normal page width without a space.

For example

```sh
cd /some/super/long/super/long/folder
```

or any other very long command.

Code snippets on my blog are all automatically added inside a `code` tag, and inside it into a `pre` tag.

By default the CSS `white-space` property on the `pre` tag is set to `normal`, and to fix this problem we set it to `pre-wrap`:

```css
pre {
  white-space: pre-wrap;
}
```
