---
title: "How to setup Tailwind with PurgeCSS and PostCSS"
description: "How I set up my workflow to trim the Tailwind CSS using PurgeCSS and a simple PostCSS setup (no webpack involved)"
date: 2018-06-30T07:06:29+02:00
updated: 2019-11-18T07:06:29+02:00
tags: css
---

I recently set out to move my blog CSS to [Tailwind](https://tailwindcss.com/).

Tailwind is an interesting framework because instead of providing a set of widgets like Bootstrap or others, it provides *utilities*.

I find it resonates a lot with how I work with HTML.

I introduced how I use [Tailwind with Vue](/vue-tailwind/) in a previous post, but without a build tool in place already, it can be hard to get the correct setup right, and I decided to write this blog post even just for me to remember later on 🙃

In this post I explain how to use Tailwind with _any_ kind of project.

## Install Tailwind

First step is to install Tailwind, using npm or yarn:

```bash
npm init -y
npm install tailwindcss
```

## Create the configuration file

Next, use this command to create a configuration file:

```bash
npx tailwind init
```

This will create a `tailwind.config.js` file in the root of your project, adding the basic Tailwind configuration.

## Configure PostCSS

Now you need to tweak the [PostCSS](/postcss/) configuration to make sure Tailwind runs. Add:

```bash
module.exports = {
  plugins: [
    require('tailwindcss'),
    require('autoprefixer')
  ]
}
```

to your `postcss.config.js`. Create one if it does not exist.

I also added autoprefixer for convenience, you'll likely need it. Install it with `npm install autoprefixer`.

Oh, also make sure you installed PostCSS (`npm install -g postcss-cli`)

## Create the Tailwind CSS file

Now create a CSS file where you want, like in  `tailwind.css` and add

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

## Create the build command

Now open your `package.json` file, and add a scripts section if you don't have it:

```json
"scripts": {
  "build:css": "postcss src/tailwind.css -o static/dist/tailwind.css"
}
```

## Build Tailwind

Now from the command line run `npm run build:css` will build the final CSS file.

The resulting file is in `static/dist/tailwind.css` (you can change the location in the above command).

## Automatically regenerate the CSS upon file changes

Every time I change something in the theme HTML (stored in the `layouts` folder in my case), I want to regenerate the CSS, and trigger the purge and minification I set up.

How to do this?

Install the [`watch`](https://www.npmjs.com/package/watch) npm package:

```bash
npm install watch
```

and add the `watch` script to your `package.json` file. You already had `build:css` from before, we just add a script that watches the layouts folder and runs `build:css` upon every change:

```json
"scripts": {
  "build:css": "postcss src/tailwind.css -o static/dist/tailwind.css",
  "watch": "watch 'npm run build:css' ./layouts"
}
```

Now run `npm run watch` and you should be good to go!

## Trim the file size

If you check, the resulting file is huge. Even if you don't use any Tailwind class in your HTML, all of the framework is included by default, because that's the default configuration in the `tailwind.js` file.

They decided to include all, to avoid people missing things. It's a design choice. We now need to **remove stuff**, and it turns out we can use purgecss to remove all the unused CSS classes.

I also want to remove all comments from the CSS and make it as small as possible. [cssnano](https://cssnano.co/) is what we're looking for.

We can automate this stuff! First, install those utilities:

```bash
npm install cssnano
npm install @fullhuman/postcss-purgecss
```

Then we add this to our PostCSS configuration file `postcss.config.js`:

```js
const purgecss = require('@fullhuman/postcss-purgecss')
const cssnano = require('cssnano')

module.exports = {
  plugins: [
    require('tailwindcss'),
    require('autoprefixer'),
    cssnano({
      preset: 'default'
    }),
    purgecss({
      content: ['./layouts/**/*.html', './src/**/*.vue', './src/**/*.jsx'],
      defaultExtractor: content => content.match(/[\w-/:]+(?<!:)/g) || []
    })
  ]
}
```

## In development, avoid too much processing

Why? Every step you add slows down the feedback cycle while developing. I use this config to only add prefixes and removing comments in production:

> `postcss.config.js`

```js
const purgecss = require('@fullhuman/postcss-purgecss')
const cssnano = require('cssnano')

module.exports = {
  plugins: [
    require('tailwindcss'),
    process.env.NODE_ENV === 'production' ? require('autoprefixer') : null,
    process.env.NODE_ENV === 'production'
      ? cssnano({ preset: 'default' })
      : null,
    purgecss({
      content: ['./layouts/**/*.html', './src/**/*.vue', './src/**/*.jsx'],
      defaultExtractor: content => content.match(/[\w-/:]+(?<!:)/g) || []
    })
  ]
}
```