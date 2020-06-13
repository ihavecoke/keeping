---
title: Use :empty pseudo-class select dom in css
published: true
description: :empty selector is intersting
tags: CSS, Tricks
cover_image: https://dev-to-uploads.s3.amazonaws.com/i/cgu0k66i5gl6ecy8yv2g.jpg
---
![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/0gtdrx8oy7f4njg3c7j1.jpg)

`:empty` pseudo-class selector can used when you need select empty dom in **CSS** let's show case

```html
<!-- will be selector -->
<div></div>
<div></div>
<div><!-- comment --></div>

<!-- will not selected if has comment with line break  -->
<div>
  <!-- comment here  -->
</div>

<!-- will not be select if contain space -->
<div> </div>

<!-- not be select if contain content-->
<div> anything </div>

<!-- will be selector -->
<div></div>
```

`:empty` just used for select **DOM** which contain nothing even comment.

[demo](https://codepen.io/ihavecoke/pen/qBbNaOq)

Hope it can help you :)
