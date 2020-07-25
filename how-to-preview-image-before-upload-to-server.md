---
title: How to preview image before upload to server 
published: true
description: 
tags: Javascript, Ticks
cover_image: https://dev-to-uploads.s3.amazonaws.com/i/3x4w194sixs68jtnh3u4.jpg
---

Recently my team have case to upload image to server i just want to show progress to user image upload status. if show the user which image file upload is more graceful. so i just preview image and show the progress same time. 

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/3k094xqhw3ela0kbrtvm.png)

Look at the screenshoot. before the image show the upload icons. direction current image uploading to server. i thinks it's more simple and useful.

```	javascript
// html code
<input id="input_file" type="file" multiple @change="fileChange" />

// here file agrument from html input file tag
covertInputImageToDataURL(file) {
  return new Promise((resolve, reject) => {
    const fr = new FileReader()
    fr.onload = () => {
      resolve(fr.result)
    }
    fr.readAsDataURL(file)
  })
}

// event listener to input file tag 
const files = []
fileChange() {
  const newFiles = document.getElementById('input_file')
  
  // covert all file to dataURL
  for (let i = 0; i < newFiles.length; i++) {
    const file = newFiles.item(i)
    const fileID = randomString() // random file id 
    const dataURL = await this.covertInputImageToDataURL(file)
		files[fileID] = { file, dataURL }
  }
} 
```

Here is Vue.js Template Define

```html
// use files 
<div v-for="key in Object.keys(files)" :key="key" >
  <img :src="files[key]['dataURL']" :alt="key" />
</div>
```

So far we just listener **input** file tag file change event and covert files to dataURL. when we set **img** `src` attribute with dataURL the image will shown by the tag. we can know which image uploading. 

Help it can help you :)


