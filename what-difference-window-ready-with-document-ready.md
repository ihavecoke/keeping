---
title: What difference window.ready with document.ready
published: true
description: window.ready vs document.ready
tags: Javascript, Tips
---

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/j0i39sv4298nsqh65onk.jpg)

`JQuery` are basically used in project, aways defined **events** callback like  `$(document).on('ready', function(){})` when document reday. but there has one things Interest me, what is different  `window.onload ` with `document.ready` ?

### window.onload

This event must wait for all elements on the page to loaded then execute this function after rendering

### document.ready

This event be executed as soon as the dom is loaded ignore other **Asset(images,videos)** if ready

Also confuse? let's talk a simple example

### Simple example

We create new chrome tab with url request page, this page havs many images.

When the page **DOM**  are loaded but images, `window.ready` won't be trigger until images loaded browser will trigger this callback

As long as page **DOM** is loaded even if image is not loaded browser will trigger  `document.ready`

### One words

`window.ready` : trigger when page all **DOM** and **Asset(images, videos)** are rendered ready

`document.ready` trigger when page loaded render process rendered even if **Asset(images, videos)** not ready

Hope it can help you :)
