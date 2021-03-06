---
title: "[Frontend] CSS, @media와 transition"
excerpt: "viewport에 따른 CSS 적용"
date: 2021-02-26
last_modified_at: 
categories:
  - Frontend
tags:
  - Frontend 
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

# Transition Example

## HTML

```html
<!DOCTYPE html>
<html>

<head>

    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>보물지도</title>
    <link rel="stylesheet" href="index.css">

</head>

<body>

<div class="map">
    <h1 id = "hint">SW마에스트로</h1>
</div>

</body>

</html>
``` 

## CSS 

```css
* {
    margin: 0;
    padding: 0;
}

html, body{
    width: 100%;
    height: 100%;
}

.map{
    background:#0000ff;
    display:table;
    width: 100%;
    height: 100%;

}

#hint{
    color:#0000ff;
    display:table-cell;
    vertical-align:middle;
    text-align:center;
    line-height: 50%;

}

@media screen  and (min-width:100px) and (max-width: 720px) {
    /* CSS that should be displayed if width is equal to or less than 800px goes here */

    .map{
        background:#00ff00;
        transition-property: background;
        transition-duration: 0.5s;
    }

    #hint{
        color:#00ff00;
        transition-property:color;
        transition-duration: 0.5s;
    }

    .map:hover {
        background:#ff0000;
    }

    #hint:hover{
        color:#ffffff;
    }
}
```

# Reference

- w3school
- [transition](https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Transitions/Using_CSS_transitions)

**Success Notice:**  
수고하셨습니다. :+1:
{: .notice--success}