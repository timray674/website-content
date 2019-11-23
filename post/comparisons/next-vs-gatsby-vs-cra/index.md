---
title: "Next.js vs Gatsby vs create-react-app"
date: 2019-11-06T07:00:00+02:00
description: "Next.js or Gatsby? Why choosing them over create-react-app? And which one?"
tags: next
---

[`create-react-app`](/react-create-react-app/) does not help you generate a server-side-rendered app easily. Anything that comes with it (SEO, speed...) is only provided by tools like [Next.js](/nextjs/) and [Gatsby](/gatsby/).

**When is Next.js better than Gatsby?**

They can both help with **server-side rendering**, but in 2 different ways.

The end result using Gatsby is a static site generator, without a server. You build the site, and then you deploy the result of the build process statically on Netlify or another static hosting site.

Next.js provides a backend that can server side render a response to request, allowing you to create a dynamic website, which means you will deploy it on a platform that can run Node.js.

Next.js _can_ generate a static site too, but I would not say it's its main use case.

If my goal was to build a static site, I'd have a hard time choosing and perhaps Gatsby has a better ecosystem of plugins, including many for blogging in particular.

Gatsby is also heavily based on [GraphQL](/graphql/), something you might really like or dislike depending on your opinions and needs.