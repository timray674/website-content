---
title: Responsive YouTube Video Embeds
date: 2019-11-17T07:00:00+02:00
description: "How to embed a YouTube video in your site and have it responsive, so it scales down on a mobile device"
tags: css
---

The problem with embedding YouTube videos is that they are an `iframe` and iframes need to be given an exact height and width otherwise they will look funky.

And we need to keep the proportions, based on the video aspect ratio.

To have a YouTube video be displayed responsive in your page, first wrap it into a container div:

```html
<div class="video-container">
  <iframe src="https://www.youtube.com/embed/klZNNUz4wPQ" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
```

Then add this CSS to your site:

```css
.video-container {
    overflow: hidden;
    position: relative;
    width:100%;
}

.video-container::after {
    padding-top: 56.25%;
    display: block;
    content: '';
}

.video-container iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
}
```

See that _magic number_, `56.25%`? That's needed as a padding when the aspect ratio of a video is 16:9. (9 is 56.25% of 16).

If your video is 4:3 for example, set it to 75%.