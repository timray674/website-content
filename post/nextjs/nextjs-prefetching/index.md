---
title: "Prefetching content in Next.js"
description: "How prefetching works in a Next.js app"
date: 2019-11-15T07:00:00+02:00
tags: next
---

In [linking 2 pages with Next.js](/link-two-pages-nextjs/) I mentioned how the `Link` Next.js component can be used to create links between 2 pages, and when you use it, Next.js **transparently handles frontend routing** for us, so when a user clicks a link, frontend takes care of showing the new page without triggering a new client/server request and response cycle, as it normally happens with web pages.

There's another thing that Next.js does for you when you use `Link`.

As soon as an element wrapped within `<Link>` appears in the viewport (which means it's visible to the website user), Next.js prefetches the URL it points to, as long as it's a local link (on your website), making the application super fast to the viewer.

This behavior is only being triggered in **production mode** (we'll talk about this in-depth later), which means you have to stop the application if you are running it with `npm run dev`, compile your production bundle with `npm run build` and run it with  `npm run start` instead.

Using the Network inspector in the DevTools you'll notice that any links above the fold, at page load, start the prefetching as soon as the `load` event has been fired on your page (triggered when the page is fully loaded, and happens after the `DOMContentLoaded` event).

Any other `Link` tag not in the viewport will be prefetched when the user scrolls and it

Prefetching is automatic on high speed connections (Wifi and 3g+ connections, unless the browser sends the [`Save-Data` HTTP Header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Save-Data).

You can opt out from prefetching individual `Link` instances by setting the `prefetch` prop to `false`:

```jsx
<Link href="/a-link" prefetch={false}>
  <a>A link</a>
</Link>
```