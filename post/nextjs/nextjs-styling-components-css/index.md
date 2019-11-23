---
title: "Styling Next.js components using CSS"
description: "How to style React components in Next.js?"
date: 2019-11-14T07:00:00+02:00
tags: next
---

How do we style React components in Next.js?

We have a lot of freedom, because we can use whatever library we prefer.

But Next.js comes with [`styled-jsx`](https://github.com/zeit/styled-jsx) built-in, because that's a library built by the same people working on Next.js.

And it's a pretty cool library that provides us scoped CSS, which is great for maintainability because the CSS is only affecting the component it's applied to.

I think this is a great approach at writing CSS, without the need to apply additional libraries or preprocessors that add complexity.

To add CSS to a React component in Next.js we insert it inside a snippet in the JSX, which start with

```js
<style jsx>{`
```

and ends with

```js
`}</style>
```

Inside this weird blocks we write plain CSS, as we'd do in a `.css` file:

```js
<style jsx>{`
  h1 {
    font-size: 3rem;
  }
`}</style>
```

You write it inside the JSX, like this:

```js
const Index = () => (
  <div>
		<h1>Home page</h1>

		<style jsx>{`
		  h1 {
		    font-size: 3rem;
		  }
		`}</style>
  </div>
)

export default Index
```

Inside the block we can use interpolation to dynamically change the values. For example here we assume a `size` prop is being passed by the parent component, and we use it in the `styled-jsx` block:

```js
const Index = props => (
  <div>
		<h1>Home page</h1>

		<style jsx>{`
		  h1 {
		    font-size: ${props.size}rem;
		  }
		`}</style>
  </div>
)
```

If you want to apply some CSS globally, not scoped to a component, you add the `global` keyword to the `style` tag:

```jsx
<style jsx global>{`
body {
  margin: 0;
}
`}</style>
```

If you want to import an external CSS file in a Next.js component, you have to first install `@zeit/next-css`:

```bash
npm install @zeit/next-css
```

and then create a configuration file in the root of the project, called `next.config.js`, with this content:

```js
const withCSS = require('@zeit/next-css')
module.exports = withCSS()
```

After restarting the Next app, you can now import CSS like you normally do with JavaScript libraries or components:

```js
import '../style.css'
```

You can also import a SASS file directly, using the [`@zeit/next-sass`](https://github.com/zeit/next-plugins/tree/master/packages/next-sass) library instead.