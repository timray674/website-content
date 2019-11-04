---
title: How to format a date in JavaScript
description: "Here's a very common task: how do you format a date with JavaScript? "
date: 2019-11-01T07:00:00+02:00
tags: js
---

Given a [Date](/javascript-dates/) object:

```js
const date = new Date('July 22, 2018 07:22:13')
```

there are lots of methods that will generate a string representing that date.

There are a few built-in ones. I list them all, along with a comment that shows a sample output:

```js
date.toString()
// "Sun Jul 22 2018 07:22:13 GMT+0200 (Central European Summer Time)"
```

```js
date.toTimeString() //"07:22:13 GMT+0200 (Central European Summer Time)"
```

```js
date.toUTCString() //"Sun, 22 Jul 2018 05:22:13 GMT"
```

```js
date.toDateString() //"Sun Jul 22 2018"
```

```js
date.toISOString() //"2018-07-22T05:22:13.000Z" (ISO 8601 format)
```

```js
date.toLocaleString() //"22/07/2018, 07:22:13"
```

```js
date.toLocaleTimeString()	//"07:22:13"
```

You are not limited to those, of course - you can use more low level methods to get a value out of a date, and construct any kind of result you want:

```js
date.getDate() //22
```

```js
date.getDay() //0 (0 means sunday, 1 means monday..)
```

```js
date.getFullYear() //2018
```

```js
date.getMonth() //6 (starts from 0)
```

```js
date.getHours() //7
```

```js
date.getMinutes() //22
```

```js
date.getSeconds() //13
```

```js
date.getMilliseconds() //0 (not specified)
```

```js
date.getTime() //1532236933000
```

```js
date.getTimezoneOffset() //-120 (will vary depending on where you are and when you check - this is CET during the summer). Returns the timezone difference expressed in minutes
```

Those all depend on the current timezone of the computer. There are equivalent UTC versions of these methods, that return the UTC value rather than the values adapted to your current timezone:

```js
date.getUTCDate() //22
date.getUTCDay() //0 (0 means sunday, 1 means monday..)
date.getUTCFullYear() //2018
date.getUTCMonth() //6 (starts from 0)
date.getUTCHours() //5 (not 7 like above)
date.getUTCMinutes() //22
date.getUTCSeconds() //13
date.getUTCMilliseconds() //0 (not specified)
```