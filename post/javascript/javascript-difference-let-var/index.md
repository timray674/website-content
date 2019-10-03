---
title: "What's the difference between using let and var in JavaScript?"
description: "When should you use let over var? And why? Let's find out!"
date: 2019-09-20T07:00:00+02:00
tags: js
---

In modern JavaScript we have 3 ways to declare a variable and assign it a value:

- `const`
- `let`
- `var`

When working with variables in JavaScript, I always default to using `const`. It guarantees the value can't be reassigned, and so it's safer to use.

But when I do need to redeclare a variable later on, I always use `let`.

I haven't used `var` in years, and to me it's just there for backwards compatibility purposes, and I always raise an eyebrow when I see it used.

Why?

First, `let` has **sensible scoping**.

The same scoping that is used in more or less all popular programming languages, block scoping, dictates that variables declared using `let` are scoped to the nearest block.

`var` instead is a bit more weird, as it has function scoping, which means that variables declared using `var` are scoped to the nearest function.

This has practical implications. For example, a variable is declared inside an `if` or used as the `for` loop iterator. Using `let` makes it local to those 2 blocks. Using `var`, however, allows the variable to be available outside of that block, which might lead to bugs.

Always use the tool that gives you the least amount of power, to make sure you have maximum control over it. *With great power comes great responsibility*.

Another reason to prefer `let` is **hoisting**. Like `const`, `let` variables are not hoisted, but they are initialized when evaluated.

`var` variables instead are hoisted to the top of the function, and as such they are available even in the lines _before_ their declaration. Weird, right?

Third reason: when you declare a `let` variable with the same name as one that already exists, you get an error (in [Strict Mode](https://flaviocopes.com/javascript-strict-mode/)).

Finally, another big difference: if you declare a `var` variable outside of any function, it's assigned to the **global object**, which means `window` inside the browser. `let` does not work in this way; the variable is available, but not attached to the global object, and so it's not reachable from outside of your file.
