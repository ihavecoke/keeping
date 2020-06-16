---
title: How to use WeakMap WeakSet in javascript.
published: true
description: what is weakmap weakset
tags: Javascript, Tricks
---

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/vz2h1x9fih7q4hdqciaq.jpg)

**Javascript** GC will collect object and release space which not used

```javascript
let obj = { name: "foo" };
obj = null;
// GC will release obj space in memory
```

But this case will not release space 

```javascript
let obj = { name: "foo" };
let maps = new Map();
maps.set(obj, "obj-value");
obj = null; // set obj to null want to release sapce
maps.get(obj) // 'obj-value'
// maps => Map(1) {{…} => "obj-value"}
```

Emmm..  we just set  `null`  to obj but not release space in memory, we can fetch the value use `maps.get(obj)` why?

If you want to release `obj` maybe you can use `WeakMap` or `WeakSet`

```javascript
let weakMap = new WeakMap();
let obj = { name: "foo" };
weakMap.set(obj, "obj-value");
console.log(weakMap.get(obj)) //=> "obj-value"
obj = null
console.log(weakMap.get(obj)) //=> undefined 
```

I think `WeakMap` more useful when you need store `object` key to map , aslo `WeakSet` too.

Hope it can help you :)




