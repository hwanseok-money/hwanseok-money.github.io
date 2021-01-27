---
title: "[TestDemo][Javascript] Click event listener"
excerpt: ""
date: 2021-01-27
last_modified_at:
categories:
  - Algorithm-Practice
tags:
  - Algorithm-Practice
  - Practice
  - "7568"
  - 덩치
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

## 문제

An image gallery is a set of images with corresponding remove buttons. This is the HTML code for a gallery with two images:

```html
<div>
  <div class="image">
    <img src="URL1">
    <button class="remove">X</button>
  </div>
  <div class="image">
    <img src="URL2">
    <button class="remove">X</button>
  </div>
</div>
```  

Implement the ImageGallery component that accepts a links prop and renders the gallery described above so that the first item in the links prop is the src attribute of the first image in the gallery. It should also implement the following logic: When the button is clicked, the image that is in the same div as the button should be removed from the gallery.

For example, after the first image has been removed from the gallery above, it's HTML code should look like this:

```html
<div>
  <div class="image">
    <img src="URL2">
    <button class="remove">X</button>
  </div>
</div>
```  

## 첫 번째 풀이

### 정답코드  

```javascript
function setup() {
  var els = document.getElementsByClassName('remove');

  for (var i = 0; i < els.length; i++) {
    els[i].addEventListener('click', function () {
      this.parentNode.remove();
    });
  }
}

// Example case. 
document.body.innerHTML = `
<div class="image">
  <img src="https://goo.gl/kjzfbE" alt="First">
  <button class="remove">X</button>
</div>
<div class="image">
  <img src="https://goo.gl/d2JncW" alt="Second">
  <button class="remove">X</button>
</div>`;

setup();

document.getElementsByClassName("remove")[0].click();
console.log(document.body.innerHTML);
```

**Success Notice:**
수고하셨습니다. :+1:
{: .notice--success}