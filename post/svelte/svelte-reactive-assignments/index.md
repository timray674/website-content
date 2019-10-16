---
title: Handling State Updates in Svelte
date: 2019-10-14T07:00:00+02:00
description: "How to use reactive assignments in Svelte to work with state updates within a component"
tags: svelte
---

One great thing about Svelte is that you don't need to do anything special to update the state of a component.

All you need is an assignment.

Say you have a `count` variable. You can increment that using, simply, `count = count + 1`, or `count++`:

```html
<script>
let count = 0

const incrementCount = () => {
	count++
}
</script>

{count} <button on:click={incrementCount}>+1</button>
```

This is nothing groundbreaking if you are unfamiliar with how modern Web frameworks handle state, but in React you'd have to either call `this.setState()`, or use the `useState()` hook.

Vue takes a more structured approach using classes and the `data` property.

Having used both, I find Svelte to be a much more JavaScript-like syntax.

We need to be aware of one thing, which is learned pretty quickly: we must also do an assignment when changing the value.

For simple values like strings and numbers, that's mostly a given, because all methods on String return new strings, and same for numbers - they are immutable.

But for arrays? We can't use methods that alter the array. Like `push()`, `pop()`, `shift()`, `splice()`... because there's no assignment. They change the inner data structure, but Svelte can't detect that.

Well, you *can* still use them, but after you've done your operation, you reassign the variable to itself, like this:

```js
let list = [1, 2, 3]
list.push(4)
list = list
```

Which is a bit counter-intuitive, but you'll quickly remember it.

Or you can use use the spread operator to perform operations:

```js
let list = [1, 2, 3]
list = [...list, 4]
```
