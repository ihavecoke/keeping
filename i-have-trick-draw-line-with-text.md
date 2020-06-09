---
title: I have trick draw line with text
published: true
description: CSS Draw line with text align center
tags: CSS, Trick

---

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/wrrgl6pp4sw3i1j68ht9.png)

Look at screenshot the red Circle line just draw a line with text **Here** sometimes UX design UI just like that. how to achieve the effect?

This is simpley requirement just need CSS Pseudo-class full code

```scss
@mixin line-with-text($text) {
  text-align: center;
  position: relative;
  border-bottom: 1px solid #ccc;
  margin: 100px 0;
  &::before {
    position: absolute;
    top: 100%;
    left: 50%;
    content: $text;
    color: pink;
    display: inline-block;
    background: white;
    transform: translate(-50%, -50%);
    padding: 0 10px;
  }
}
.line {
  @include line-with-text("Here");
}

```

You can copy the Snippet to you project and replace the argument `Here` all is done. also you can custom all the `mixin`  attributes.

Here is [line-with-text](https://codepen.io/ihavecoke/pen/pogjyRK) online dem, Hope it can help you :)




