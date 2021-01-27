---
title: "[TestDemo][CSS] circle border"
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

Update the website's HTML to make use of semantic elements so that:

1. The classless outer div element is replaced with a more appropriate element.
1. The divs with the image and caption classes are replaced with self-contained content elements.
The divs with the lorem-ipsum and description classes are replaced with elements, so that by default only the contents of the description element are shown. When the contents of the description element are clicked, the visibility of the rest of the lorem-ipsum element is toggled.  


## 첫 번째 풀이

### 정답코드  

```css
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Semantics</title>
  </head>
  <body>
    <main>
      <h1>Lorem Ipsum</h1>
      
      <figure class="image">
        <img src="https://goo.gl/zF9eky" alt="Lorem Ipsum">
        <figcaption class="caption">Lorem Ipsum</div>
      </figure>
      <details class="lorem-ipsum">
        <summary class="description">Lorem ipsum dolor sit amet, consectetur adipiscing elit...</summary>
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. 
          Curabitur vitae hendrerit mauris. Lorem ipsum dolor sit amet, consectetur adipiscing elit. 
          Mauris lacinia scelerisque nibh nec gravida. 
          Duis malesuada nec nibh sit amet pulvinar. 
          Phasellus congue porttitor arcu, ut suscipit nibh aliquam vel. 
          Nunc arcu lectus, egestas ut sem ac, euismod porttitor eros. 
          Phasellus tincidunt consequat pharetra. Maecenas sodales purus at nulla finibus dapibus. 
          Nullam varius at nisl vel euismod. Fusce aliquet ligula non tempor fermentum. 
          Nam fermentum posuere mauris, quis aliquam nibh dictum sed.</p>
      </details>
    </main>
  </body>
</html>
```

**Success Notice:**
수고하셨습니다. :+1:
{: .notice--success}