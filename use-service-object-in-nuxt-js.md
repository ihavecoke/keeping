---
title: Use service object in nuxt.js
published: true
description: how to user service object in nuxt.js 
tags: javascript, nuxtjs, tricks
---

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/0lzcgl0sy9qx4wuevohr.jpg)

`Nuxt.js` awesome **SSR** framwork use in my team, we use **axios** lib to request http and deal with response.

Also we use **Vuex** to store state data between component and pages.  

We just use **service** to wrap **axios** request, so that we can write logic more robust. let's show you some code 


### ApplicationService class

```javascript
// ApplicationService.js

import extend from 'lodash/extend'
import { compact } from 'lodash'
import { environment } from '../config'

const querystring = require('querystring')

class ApplicationService {
  constructor(ctx) {
    this.cache = ctx.cache
    this.logger = ctx.app.$logger
    this.axios = ctx.$axios
  }
  get(path, params = {}, extraConf = {}) {
    return this.request(path, 'GET', params, extraConf)
  }
  
  post(path, data, extraConfig = {}) {
    return this.request(path, 'POST', data, extraConfig)
  }

  put(path, data, extraConf = {}) {
    return this.request(path, 'PUT', data, extraConf)
  }

  delete(path, data = {}, extraConf = {}) {
    return this.request(path, 'DELETE', data, extraConf)
  }

  extraResp(response) {
    const data = (response && response.data) || {}
    return (data && data.data) || { err: true, code: data.code, message: data.message }
  }

  async request(path, method = 'GET', paramsData = {}, extraConfig = {}) {
    const { axios } = this
    const config = extend({method,url: path,responseType: 'json'},extraConfig,)
    try {
      const response = await axios(config)
      return this.extraResp(response)
    } catch (err) {
      console.warn('application Service', err)
      return { err: true }
    }
  }
}

export default ApplicationService

```

### UserService.js

``` javascript
import get from 'lodash/get'
import ApplicationService from './ApplicationService'

export default class UserService extends ApplicationService {
  // fetch users list
  users() {
    return this.get('/users')
  }
  
  // find user by userId
  user(userId){
    return this.get(`/users/${userId}`)
  }
}

```



### Inject  to nuxt.js global variable

```javascript
// ~/plugins/service.js

import UserService from 'UserService.js'

export default (ctx, inject) => {
  ctx.userService = new UserService(ctx)
  inject('userService', ctx.userService)
}

// we can call userService 
this.$userService.users()
this.$userService.user(1)
```



### UserServiceTest.js

```javascript
import service from 'UserService.js'

test('users', async () => {
  const data = [{name: 'foo', age: 23}]
  service.mockResponse({ data })
  const users = await service.users()
  service.expectCalledWith({ url: '/users' })
  expect(users).toEqual([{name: 'foo', age: 23}])
})
```

OK, so far you can write independent **UserServiceTest.js** and test work on.

Do that you have benefit:

* service object just care how to fetch resource from remote server
* write more clean and independent test file
* call **service** with nuxt global object `context` with `this.$service.user` 

Hope it can help you :)
