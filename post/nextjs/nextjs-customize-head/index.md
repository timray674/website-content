---
title: "Next.js: populate the head tag with custom tags"
description: "How to customize the `head` tag of your Next.js app"
date: 2019-11-19T07:00:00+02:00
tags: next
---

From any Next.js page component, you can add information to the page header.

This is handy when:

- you want to customize the page title
- you want to change a meta tag

How can you do so?

Inside every component you can import the `Head` component from `next/head` and include it in your component JSX output:

```js
import Head from 'next/head'

const House = props => (
  <div>
    <Head>
      <title>The page title</title>
    </Head>
    {/* the rest of the JSX */}
  </div>
)

export default House
```

You can add any HTML tag you'd like to appear in the `<head>` section of the page.

When mounting the component, Next.js will make sure the tags inside `Head` are added to the heading of the page. Same when unmounting the component, Next.js will take care of removing those tags.