---
title: "How to export functions and variables from a Svelte component"
date: 2019-10-02T07:00:00+02:00
description: "Learn how to export functions and variables from a Svelte component"
tags: svelte
---

You know that you can import a Svelte component into another using the syntax

```html
<script>
import Button from './Button.svelte';
</script>
```

What if you want to export something more than the default export?

Well, you must export it from a special `script` tag into the component, with the `context="module"` attribute.

Here's an example. Say you have a Button component in `Button.svelte`:

```html
<button>A button</button>
```

and you want to provide other components the ability to change the color of the button. You could use props, that's one example. Or you can provide a function, called `changeColor`.

You write and export it in this special `script` tag:

```html
<script context="module">
export function changeColor() {
  //...add logic..
}
</script>

<button>A button</button>
```

> Warning: I did not implement the actual functionality, but you get the idea.

Note that you can have another "normal" script tag, in the component.

Now other components can import Button, which is the default export, and the `changeColor` function too:

```html
<script>
import Button, { changeColor } from './Button.svelte'
</script>
```
