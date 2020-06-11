---
title: Interesting header progress navbar in dev.to
published: true
description: how to create process navbar in page header like dev.to
tags: Javascript, CSS, Tricks

---

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/mdk0wauafk53gglix1xm.jpg)


Found Interesting things when you click a link in `dev.to`  you will see a colorful progress navbar grow width it's so cool.

I just inspect how dev.to implement it. let's show code i have found:

First defined html dom like this

```html
<div class="navigation-progress showing" id="navigation-progress"></div>
```

Then use css **animate* attributes

```css
// defined background with linear-gradient 
.navigation-progress {
    position: fixed;
    top: 0;
    background: linear-gradient(to right, orange, yellow, green, cyan, blue, violet);
    z-index: 102;
    height: var(--su-1);
    width: 0%;
}
// play animation when navigation-progress dom added showing class
.navigation-progress.showing {
    display: block;
    width: 140%;
    -webkit-animation: grow-width 3200ms ease-out, pulsate 1.4s infinite ease-in-out;
    animation: grow-width 3200ms ease-out, pulsate 1.4s infinite ease-in-out;
}

// define keyframes
@keyframes grow-width {
  from {
    width: 0;
  }
  to {
    width: 100%;
  }
}
```

These CSS defined animation `grow-width` will infinite play until page loaded.

Hope it can help you :)  [Demo](https://codepen.io/ihavecoke/pen/yLeOOzP) 


