---
title: "How to import components in Svelte"
date: 2019-10-01T07:00:00+02:00
description: "Learn how to import components in Svelte"
tags: svelte
---

Svelte provides single file components. Every component is declared into a `.svelte` file, and in there you can write the HTML markup, the CSS and the JavaScript needed.

Here's a simple Svelte component example, living in a file called `Button.svelte`:

```html
<button>A button</button>
```

You _can_ add CSS and JS to this component, but this plain HTML markup is already the markup of the component, there's no need to wrap it in another special tag or anything.

To export this markup from this component you don't have to do anything. You can now import it into any other Svelte component using the `import ComponentName from 'componentPath'` syntax:

```html
<script>
import Button from './Button.svelte';
</script>
```

And now you can use the newly imported component in the markup, like an HTML tag:

```html
<Button />
```
