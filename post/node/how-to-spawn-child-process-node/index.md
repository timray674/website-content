---
title: How to spawn a child process with Node.js
date: 2019-09-27T07:00:00+02:00
description: "Find out how to spawn a child process with Node.js"
tags: node
---

Node.js provides a `child_process` module that provides the ability to spawn child processes.

Require the module, and get the `spawn` function from it:

```js
const { spawn } = require('child_process')
```

then you can call `spawn()` passing 2 parameters.

The **first parameter** is the command to run.

The **second parameter** is an array containing a list of options.

Here's an example:

```js
spawn('ls', ['-lh', 'test'])
```

In this case you run the `ls` command with 2 options: `-lh` and `test`. This results in the command `ls -lh test`, which (given that the `test` file exists, in the same folder you run this command in, results in the details about the file:

```sh
-rw-r--r--  1 flaviocopes  staff     6B Sep 25 09:57 test
```

The result of the `spawn()` function call is an instance of the `ChildProcess` class that identifies the spawned child process.

Here's a slightly more complicated example, fully working. We watch the `test` file and whenever it's changed, we run the `ls -lh` command on it:

```js
'use strict'

const fs = require('fs')
const { spawn } = require('child_process')
const filename = 'test'

fs.watch(filename, () => {
  const ls = spawn('ls', ['-lh', filename])
})
```

There's one thing missing. We must pipe the output from the child process to the main process, otherwise we won't see any output from it.

We do so by calling the `pipe()` method on the `stdout` property of the child process:

```js
'use strict'

const fs = require('fs')
const { spawn } = require('child_process')
const filename = 'test'

fs.watch(filename, () => {
  const ls = spawn('ls', ['-lh', filename])
  ls.stdout.pipe(process.stdout)
})
```
