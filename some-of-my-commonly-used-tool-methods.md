---
title: Some of my commonly used tool methods
published: true
description: 
tags: CSS, Javascript, Ticks
---

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/boz1q9nq5oxipnmtv07a.jpg)

### ellipsis text

```scss
@mixin ellipsis($line) {
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: $line;
  -webkit-box-orient: vertical;
}

.desc{
 @include ellipsis(2) // over 2 line will be fold and show ...
}
```



### Safe decimal

```javascript
import Decimal from 'decimal.js-light'

export default function(value) {
  return new Decimal(value || 0)
}

new Decimal(null) // will be new Decimal(0)
```



### Vuex extend

```javascript
import isArray from 'lodash/isArray'
import Vue from 'vue'

export function setState({ commit }, attrs, value = null) {
  commit('mutationState', attrs, value)
}

/*
 * setState('key',value)
 * setState(['key','value'])
 * setState({key: 'key', value: 'value'})
 * setState([{key: 'key', value: 'value'}])
 */
export function mutationState(state, attrs, value = null) {
  if (value) {
    Vue.set(state, attrs, value)
  } else if (isArray(attrs)) {
    // [{key: 'xx', value: 'xx'}, ['key', 'value']]
    while (attrs.length) {
      const ele = attrs.pop()
      if (isArray(ele)) {
        const [key, value] = ele
        Vue.set(state, key, value)
      } else {
        const { key, value } = ele
        Vue.set(state, key, value)
      }
    }
  } else {
    // setState({key: 'key', value: 'value'})
    const { key, value } = attrs
    Vue.set(state, key, value)
  }
}

// store/user.js
import { mutationState, setState } from '@/utils/vuex'
export const actions = {
  setState
}
export const mutations = {
  mutationState
}

this.$store.dispatch("user/setState",data)
```

 You can use `setState` method to update vuex state values 



### Generate utils class in scss

```scss
@for $i from 1 through 8 {
  .mt-#{$i*4} {
    margin-top: #{$i * 4}px !important;
  }
  .mb-#{$i*4} {
    margin-bottom: #{$i * 4}px !important;
  }
  .pb-#{$i*4} {
    padding-bottom: #{$i * 4}px !important;
  }
  .pt-#{$i*4} {
    padding-top: #{$i * 4}px !important;
  }
  .ml-#{$i*4} {
    margin-left: #{$i * 4}px !important;
  }
  .mr-#{$i*4} {
    margin-right: #{$i * 4}px !important;
  }
}

// will out put css
.mt-4{margin-top:4px}
.mb-4{margin-bottom:4px}
.ml-4{margin-left:4px}
.mr-4{margin-right:4px}
...
.mt-32{margin-top:32px}
.mb-32{margin-bottom:32px}
.ml-32{margin-left:32px}
.mr-32{margin-right:32px}

.pt-4{padding-top:4px}
...
.pt-32{padding-top:32px}

.pb-4{padding-bottom:4px}
...
.pb-32{padding-bottom:32px}
```



More tips you can share in comments



Hope it can help you :)
