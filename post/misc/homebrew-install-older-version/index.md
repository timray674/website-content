---
title: How to install an older version of a Homebrew package
date: 2019-09-19T07:00:00+02:00
description: "Installing an older version of some package using Homebrew can be more complex than you expect"
---

I had this problem: I updated Hugo, which is the CMS I use, and one of the versions that were more recent than the one I used introduced a breaking change.

My homepage didn't list the blog posts any more. I didn't have the time to figure out _why_, so I said "I'll just roll back".

Now the question became.. "how?"

First, I uninstalled Hugo:

```sh
brew unlink hugo
```

Then I followed the instructions I found on [this post](https://www.fernandomc.com/posts/brew-install-legacy-hugo-site-generator/). I had to search for the Hugo package formula  [https://github.com/Homebrew/homebrew-core/search?utf8=%E2%9C%93&q=hugo&type=](https://github.com/Homebrew/homebrew-core/search?utf8=%E2%9C%93&q=hugo&type=) then I clicked that file (`Formula/hugo.rb`), and I pressed the History button to see all the previous versions.

Navigated to the 0.53 version I wanted and I clicked the `<>` button to see the `homebrew-core` repository at that point in time. Then I opened the `Formula/hugo.rb` file, and I clicked `Raw` to get the direct URL to that file.

I then used it as the argument for `brew install`. For example:

```sh
brew install https://raw.githubusercontent.com/Homebrew/homebrew-core/5441fa16872c9a56bd5997558df45b808f13285b/Formula/hugo.rb
```

That's it.

My next step for solving the problem I had was to uninstall the current version installed, and trying to update one version at a time, so I could isolate the release that introduced the change that was causing me problems.