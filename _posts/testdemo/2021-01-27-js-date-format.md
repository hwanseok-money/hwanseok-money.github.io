---
title: "[TestDemo][Javascript] format from M/D/YYYY to YYYYMMDD"
excerpt: ""
date: 2021-01-27
last_modified_at:
categories:
  - TestDemo
tags:
  - TestDemo
  - Practice
  - "7568"
  - 덩치
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

## 문제

Write a function that converts user entered date formatted as M/D/YYYY to a format required by an API (YYYYMMDD). The parameter "userDate" and the return value are strings.

For example, it should convert user entered date "12/31/2014" to "20141231" suitable for the API.

## 첫 번째 풀이

```javascript
const date1 = new Date('1995-12-17')
console.log
```

### 정답코드  

```javascript
function formatDate(userDate) {
  userDate = new Date(userDate);
  y = userDate.getFullYear().toString();
  m = (userDate.getMonth() + 1).toString();
  d = userDate.getDate().toString();
  if(m.length == 1) m = '0' + m;
  if(d.length == 1) d = '0' + d;
  return y+m+d;
}

console.log(formatDate("12/31/2014"));
```

**Success Notice:**
수고하셨습니다. :+1:
{: .notice--success}