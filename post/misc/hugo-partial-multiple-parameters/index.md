---
title: How to pass multiple parameters to a partial in Hugo
date: 2019-09-18T07:00:00+02:00
description: "How do you pass multiple parameters to a partial in Hugo? It's not as simple as it seems, you need to use a trick. Let's find out."
---

I use Hugo to manage this site. It's pretty cool.

One thing that got me stuck today was passing 2 parameters to a partial.

Since in a partial I could not access `.Site.Pages` to get the list of pages of the site (due to scope issues), I had to create a dictionary and fill it with 2 items:

```go
{{ partial "my-partial.html" (dict "context" . "pages" $.Site.Pages) }}
```

The key here is passing `(dict "context" . "pages" $.Site.Pages)` as the parameter, instead of `.` as you usually do with partials.

Now inside the partial, instead of using `.` to access the current context variables you'd use `.context`.

And to access the value assigned to `pages`, I'd use `.pages`.

You can of course pass multiple items, too. Just add more items to the `dict`.