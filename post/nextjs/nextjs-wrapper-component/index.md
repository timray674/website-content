---
title: "Adding a wrapper component to your Next.js app"
description: "How to use a wrapper component and add a common sidebar or header to it"
date: 2019-11-25T07:00:00+02:00
tags: next
---

All the pages on your site look more or less the same. There's a chrome, a common base layer, and you just want to change what's inside.

There's a nav bar, a sidebar, and then the actual content.

How do you build such system in Next.js?

There are 2 ways. One is using a [Higher Order Component](https://flaviocopes.com/react-higher-order-components/), by creating a `components/Layout.js` component:

```js
export default Page => {
  return () => (
    <div>
      <nav>
        <ul>....</ul>
      </hav>
      <main>
        <Page />
      </main>
    </div>
  )
}
```

In there we can import separate components for heading and/or sidebar, and we can also add all the CSS we need.

And you use it in every page like this:

```js
import withLayout from '../components/Layout.js'

const Page = () => <p>Here's a page!</p>

export default withLayout(Page)
```

But I found this works only for simple cases, where you don't need to call `getInitialProps()` on a page.

Why?

Because `getInitialProps()` gets only called on the page component. But if we export the Higher Order Component withLayout() from a page, `Page.getInitialProps()` is not called. `withLayout.getInitialProps()` would.

To avoid unnecessarily complicating our codebase, the alternative approach is to use props:

```js
export default props => (
  <div>
    <nav>
      <ul>....</ul>
    </hav>
    <main>
      {props.content}
    </main>
  </div>
)
```

and in our pages now we use it like this:

```js
import Layout from '../components/Layout.js'

const Page = () => (
  <Layout content={(
    <p>Here's a page!</p>
  )} />
)
```

This approach lets us use `getInitialProps()` from within our page component, with the only downside of having to write the component JSX inside the `content` prop:

```js
import Layout from '../components/Layout.js'

const Page = () => (
  <Layout content={(
    <p>Here's a page!</p>
  )} />
)

Page.getInitialProps = ({ query }) => {
  //...
}
```