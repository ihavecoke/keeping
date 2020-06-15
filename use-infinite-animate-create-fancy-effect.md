---
title: Use infinite animate create fancy effect
published: true
description: infinite animate in css
tags: CSS,Tricks,Animation
---

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/9b384tzq70bv2pxmx2m8.jpg)

I have feature should show stocks indeics auto infinite scroll.  first i want to use javascript to controll it. but other developer told me we can use CSS animation create this，it's cool let's me show you code below.

```vue
<template>
  <div class="marquee">
    <div class="marquee" :style="{ width: `${width}px`, height: `${height}px` }">
      <div class="marquee--inner">
        <div class="group">
          <slot />
        </div>
        <div class="group">
          <slot />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import PropTypes from 'vprop-type'
export default {
  name: 'Marquess',
  props: {
    width: PropTypes.integer,
    height: PropTypes.integer.def(20),
    itemKlass: PropTypes.string.def('item'),
    speed: PropTypes.integer.def(8) // 5s
  }
}
</script>

<style scoped lang="scss">
@import '_variable.scss';
.lb-marquee {
  overflow: hidden;
  -webkit-transform: translateZ(0);
  -moz-transform: translateZ(0);
  -ms-transform: translateZ(0);
  -o-transform: translateZ(0);
  transform: translateZ(0);
  .marquee {
    width: 100%;
    overflow: hidden;
    box-sizing: border-box;
    position: relative;
  }
  .marquee--inner {
    display: block;
    width: 200%;
    margin: $gutter-sm 0;
    position: absolute;
    // keywords
    animation: marquee 40s linear infinite; 
  }

  .marquee--inner:hover {
    animation-play-state: paused;
  }

  .group {
    float: left;
    width: 50%;
    .item {
      width: 100px;
      display: inline-block;
      float: left;
    }
  }

  @keyframes marquee {
    0% {
      left: 0;
    }
    // here is keywords
    100% {
      left: -100%;
    }
  }
}
</style>

```

That all you can use the Vue component like this:

```vue
<Marquess :width="210 * 8" :height="140">
  <div v-for="(item, index) in  items" :key="item.id" :index="index" class="item" :style="{ width: '210px' }">
    ......
  </div>
</Marquess>
```

I have videos to show what the component is [demo](http://public.mixbo.cn/screen-capture.webm)

Hope it can help you :)
