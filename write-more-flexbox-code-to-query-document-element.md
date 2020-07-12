---
title: write more flexbox code to query document element.
published: true
description: 
tags: javascript, ticks
---

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/yit35qu0jjaa7m0dpocg.jpg)


Sometimes you need check if HTML element present in **document**, special your dom load from remote server and dynamic add to document. 

If you code query **DOM** when document loaded, firt time the **DOM** maybe present you can queried it.

But if your **DOM** load from server, you query code clound not found it anymore. becuase you query code execute before  **DOM **add to document

How reslove it?  show me code to you

```javascript
const awaitSomethingReady = (condition, maxCount = 500) => {
  return new Promise((resolve, reject) => {
    let getTestIntervalId = null
    const maxCheckCount = maxCount || 500
    let currentCheckCount = 0
    getTestIntervalId = setInterval(() => {
      currentCheckCount += 1
      if (maxCheckCount === currentCheckCount) {
        clearInterval(getTestIntervalId)
        reject()
      }
      if (condition()) {
        clearInterval(getTestIntervalId)
        resolve()
      }
    }, 50)
  })
}
```

I just want to check if **div** with calss **toolbar** present so use `awaitSomethingReady`

```javascript
awaitSomethingReady(document.querySelector(".toolbar")).then(()=>{
  console.log("found toolbar")
}).catch(()=>{
  console.log("will found toolbar continue ...")
})
```

That all you will write more flexible code 

Hope it can help you 


