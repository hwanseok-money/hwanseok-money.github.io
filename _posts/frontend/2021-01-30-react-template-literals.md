---
title: "[React] Template Literals"
excerpt: ""
date: 2021-01-30
last_modified_at: 
categories:
  - Frontend
tags:
  - Frontend 
  - React
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

**Info Notice:**  
안녕하세요. **HwanSeok**입니다.  
본 포스팅은 React의 기초 개념을 다지는 포스팅입니다.  
{: .notice--info}

# Template Literals

```javascript
return newItems.map(item => (
    <li
        key={item.id}
        className="list-group-item d-flex justify-content-between align-items-center"
    >
    <span
        className={`todo-title mr-2 ${
            this.state.viewCompleted ? "completed-todo" : ""
        }`}
        title={item.description}
    >
      {item.title}
    </span>
    </li>
));
```  

위 코드에서 ${}로 된 부분이 있습니다. 이 부분은 템플릿 리터럴입니다.  

템플릿 리터럴은 내장된 표현식을 허용하는 문자열 리터럴입니다. 여러 줄로 이뤄진 문자열과 문자 보간기능을 사용할 수 있습니다. 이전 버전의 ES2015사양 명세에서는 "template strings" (템플릿 문자열) 라고 불려 왔습니다.

# Reference

- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Template_literals

**Success Notice:**  
수고하셨습니다. :+1:
{: .notice--success}