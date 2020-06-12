---
title: Use colorful avatar improve user experience 
published: true
description: We can use default name alphabet to holding avatar if user not setting.
tags: Javascript, Tricks, HTML
---

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/gwajd7xyh139ppnw49ra.jpg)

I develop **Vue** component to show user avatar, below screenshoot show component is.

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/19k3c1hbdmawkkapae0v.png)

As you can see has two circle avatar one show **M** alphabet and other shown **image**.

```html
// show first alphabet from mixbo 
<Avatar name="mixbo"/> 

// show image with src url
<Avatar src="https://dev-to-uploads.s3.amazonaws.com/i/gwajd7xyh139ppnw49ra.jpg" />
```

I think it helpful when show user avatar but user not upload avatar, it's good experience isn't it? 

Also you can use default avatar image when user not upload avatar.

The different alphabet  avatar  to default avatar is more personal and colorful.

Show you how to calculate the first alphabet with different background color

```javascript
const colors = [
  '#414656',
  '#F6C100',
  '#BD66CC',
  '#FF4B4B',
  '#00B8D4',
  '#2F70FF',
  '#3BB46E',
  '#00838f',
  '#0091EA',
  '#FF6D00',
  '#9a6157',
  '#333333',
]
avatarAlphabetBGColor = (name) => {
  const idx = name.charCodeAt(0) % colors.length
  return colors[idx]
}
avatarAlphabetBGColor("mixbo") // "#F6C100"
```

`avatarAlphabetBGColor` caculate the first name aplhabet and get the background color from pre-define const `colors`. so same aplhabet will return same background color. 

```java
avatarAlphabetBGColor("mixbo") // "#F6C100"
avatarAlphabetBGColor("mile") // "#F6C100"
avatarAlphabetBGColor("ihavecoke") // "#FF6D00"
```

That all the magical hope it can help you :)

