---
title: "Svelte templates: conditional logic"
date: 2019-10-03T07:00:00+02:00
description: "Learn how to work with templates in Svelte and in particular how to use conditionals"
tags: svelte
---

Any good templating language for the Web provides you at least 2 things: a conditional structure, and a loop.

Svelte is no exception, and in this post I'll look into conditional structures.

You want to be able to look at a value/expression, and if that points to a true value do something, if that points to a false value then do something else.

Svelte provides us a very powerful set of control structures.

The first is **if**:

```html
{#if isRed}
	<p>Red</p>
{/if}
```

There is an opening `{#if}` and an ending `{/if}`. The opening markup checks for a value or statement to be truthy. In this case `isRed` can be a boolean with a `true` value:

```html
<script>
let isRed = true
</script>
```

An empty string is falsy, but a string with some content is truthy.

0 is falsy, but a number > 0 is truthy.

The boolean value `true` is truthy, of course, and `false` is falsy.

If the opening markup is not satisfied (a falsy value is provided), then nothing happens.

To do something else if that's not satisfied, we use the appropriately called `else` statement:

```html
{#if isRed}
	<p>Red</p>
{:else}
	<p>Not red</p>
{/if}
```

Either the first block is rendered in the template, or the second one. There's no other option.

You can use any JavaScript expression into the `if` block condition, so you can negate an option using the `!` operator:

```html
{#if !isRed}
	<p>Not red</p>
{:else}
	<p>Red</p>
{/if}
```

Now, inside the `else` you might want to check for an additional condition. That's where the `{:else if somethingElse}` syntax comes along:

```html
{#if isRed}
  <p>Red</p>
{:else if isGreen}
  <p>Green</p>
{:else}
  <p>Not red nor green</p>
{/if}
```

You can have many of these blocks, not just one, and you can nest them. Here's a more complex example:

```html
{#if isRed}
  <p>Red</p>
{:else if isGreen}
  <p>Green</p>
{:else if isBlue}
  <p>It is blue</p>
{:else}
  {#if isDog}
    <p>It is a dog</p>
  {/if}
{/if}
```
