---
title: Use iconfront to create icon component
published: true
description: 
tags: Javascript, Vue, Tricks

---

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/5lyj2r9j3y6lb68ul0x8.jpg)

How to create `icon` component with [iconfront](https://www.iconfont.cn/) let show you code simple and clearn

### icon.vue

```vue
<template>
  <svg
    class="icon iconfont"
    aria-hidden="true"
    :class="name"
    @click="
      () => {
        this.$emit('click')
      }
    "
  >
    <use :xlink:href="`#icon-${name}`"></use>
  </svg>
</template>

<script>
export default {
  props: {
    name: {
      type: String,
      required: true
    }
  }
}
</script>

<style>
.icon {
  -webkit-font-smoothing: antialiased;
  -webkit-text-stroke-width: 0.2px;
  width: 1em;
  height: 1em;
  vertical-align: -0.15em;
  fill: currentColor;
  overflow: hidden;
}
</style>

```

### demo.vue

```vue
<template>
  <div class="container">
    <icon name="add" />
    <icon name="circle" />
  </div>
</template>
<script>
import Icon from './index'
export default {
  components: {
    Icon
  },
  methods: {
    toast() {
      alert('click')
    }
  }
}
</script>
<style lang="scss" scoped>
.icon {
  width: 24px;
  height: 24px;
  margin: 8px;
}
.hide-right {
  color: $primary;
}
</style>

```

Download iconfront static files and import to you project, that all.


Hope it can help you :)
