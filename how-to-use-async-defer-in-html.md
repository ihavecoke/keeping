---
title: How to use async, defer in html
published: true
description: 
tags: Javascript, Tricks
---
![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/ankhzl30y2qymp0ks667.jpg)

When the browser loads HTML and comes across a `<script>...</script>` tag, it can’t continue building the DOM. It must execute the script right now. The same happens for external scripts `<script src="..."></script>`: the browser must wait until the script downloads, execute it, and only after process the rest of the page.

There are two `<script>` attributes that solve the problem for us: `defer` and `async`.

### defer

The `defer` attribute tells the browser that it should go on working with the page, and load the script “in background”, then run the script when it loads.

### async

The `async` attribute means that a script is completely independent:

- The page doesn’t wait for async scripts, the contents are processed and displayed.
- DOMContentLoaded and async scripts don’t wait for each other:
  - `DOMContentLoaded` may happen both before an async script (if an async script finishes loading after the page is complete)
  - …or after an async script (if an async script is short or was in HTTP-cache)
- Other scripts don’t wait for `async` scripts, and `async` scripts don’t wait for them.

So, if we have several `async` scripts, they may execute in any order. Whatever loads first – runs first

Hope it can help you :)

Cherry pick from [concept](https://javascript.info/script-async-defer#defer)


