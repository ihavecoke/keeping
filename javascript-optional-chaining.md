---
title: javascript optional chaining
published: true
description: how to fetch object safe
tags: Javascript, Tricks
---
![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/4q56d1194l88u8kkyvzu.jpg)

You may write code in **javascript** like this:

```javascript
if (foo && foo.bar && foo.bar.baz) {
	foo.bar.baz();
}
```

We want to call `baz()` but first need check if `foo` , `foo.bar`, `foo.bar.baz`  present.  i think this is a little bit more prolixity. 

Now you can write code like 

```javascript
foo?.bar?.baz() 
```

That all, just need use `?.` operator, this called **optional chainning**.  you need do something in **babel** config 

```javascript
// babel.config.js
module.exports = {
  env: {
  		.....
      plugins: ['@babel/plugin-proposal-optional-chaining']
    }
  }
}
```

### More **optional Channing** example:

#### Dealing with optional callbacks or event handlers

```javascript
function doSomething(onContent, onError) {
  try {
   // ... do something with the data
  }
  catch (err) {
    onError?.(err.message); // no exception if onError is undefined
  }
}
```

#### Optional chaining with expressions

```javascript
let nestedProp = obj?.['prop' + 'Name'];
```

#### Array item access with optional chaining

```javascript
let arrayItem = arr?.[42];
```



You can found more api [optional chainning](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining)

Hope it can help you :)


