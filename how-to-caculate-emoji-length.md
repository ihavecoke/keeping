---
title: How to caculate emoji length?
published: true
description: The way i found to get emoji length
tags: Javascript, Tricks
---

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/17dv57h61f19kqq39d2c.jpg)

In Javascript we just call `length` on String object will return the **length** you want to get.

But when you get **emoji** length from **javascript** become more trouble let show you what i found.

```javascript
"ihavecoke".length // 9

"😁".length // 2
```

As you can see, when you call `length` on `'ihavecoke'`  you got length **9** it's ture and make sense.

The line number 3 you just got length **2**. what ? a emoji char just **2** length of string?

The `"👨‍👨‍👧‍👦".length`  more strange that return **11** why ? emoji char not return **2** always?



So how to caculate emoji length to **1** length?  you can you lodash method `toArray` it's simple and useful ways

```javascript
_.toArray("😁").length // 1

_.toArray("👨‍👨‍👧‍👦").length // 1

_.toArray("ihavecoke 🤩").length // 11
```



So we got the **1** length emoji lols 



Hope it can help you :)


