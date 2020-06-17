---
title: Javascript Array methods used in my work
published: true
description: useful array methods in javascript
tags: Javascript,Tricks
---
![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/t15b93lvyanr2d7v1qws.jpg)

Here list some `Javascript` Array methods witch helpful and useful to my work

### some & every

```javascript
let users = [{name: 'foo',age: 18},{name: 'bar',age: 21}]
users.some((user)=>user.age < 20) // true
users.every((user)=>user.age < 20) // false
```

* `some` just return `true` if `users` has one user age < 20
* `every` just return true if all `users` age < 20 



### splice

```javascript
// splice(index[, deleteCount, elem1, ..., elemN])
const fruits = ['apple','pera','grape']
fruits.splice(1,1,'pineapple','watermelon') // ['pera']
// fruits: ['apple','pineapple','watermelon','grape']
```

`splice` method will return modified array elements but will mutation origin array. `fruits` will be `['apple','pineapple','watermelon','grape']`

Args

* `index` which started index you will mutation
* `deleteCount` will declare how many element you will replaced
* `elem1,...eleN` will after `index` poistion



### unshift & push

```javascript
const fruits = ['apple','pera','grape']

fruits.unshift(...['pineapple']) // will return fruits length 4
console.log(fruits) // (4) ["pineapple", "apple", "pera", "grape"]

fruits.push('watermelon')  // will return fruits length 5
console.log(fruits) //(5) ["pineapple", "apple", "pera", "grape", "watermelon"]
```



* `unshfit(...item)` will push item to beginning of array
* `push(item)` will push item to end of array



### forEach

```javascript
["foo", "bar", "zzzzz"].forEach((item, index, array) => {
  console.log(`${item} is at index ${index} in ${array}`);
});
```

Usual we just pass first two args `item`, `index` but `array` used when you need referer  the iterate object here is `["foo", "bar", "zzzzz"]` 



### find & findIndex

```javascript
const fruits = ['apple','pera','grape']

fruits.find((fruit)=> fruit==='apple') // apple
fruits.findIndex((fruit)=> fruit==='grape') // 2

// if not found will return -1
fruits.findIndex((fruit)=> fruit==='notfound') // -1
```

* `find` will return the first matched element in `fruits`
* `findIndex` will return the first matched element index at `fruits` array



### filter

```javascript
const fruits = ['apple','pera','grape']
let results = fruits.filter((fruit) => fruit.length > 4) // (2) ["apple", "grape"]
```

`fileter` will return new array witch iterate callback return `true`



### map

```javascript
let items = ["foo", "bar", "zzz"].map(item => `lol:${item}`);
console.log(items); // (3) ["lol:foo", "lol:bar", "lol:zzz"]
```

We can use `map` transform array element and return new array



Not limited to the above method aslo includes: `reverse`, `reduce`, `concat` ,`slice` ,  `join`



Hope it can help you :)
