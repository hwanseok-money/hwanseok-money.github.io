---
title: "[Tips] excel table을 markdown으로 변환하기"
excerpt: ""
date: 2021-01-03
categories:
  - Tips
tags:
  - Tips
  - excel
  - table
  - markdown
  - convert
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true

---

## 문제 상황

github 포스팅을 할 때 markdownd을 자주 사용하는데요, 테이블을 일일이 적는 과정이 무척 번거롭습니다. 이러한 경우 아래의 사이트를 이용하면 쉽게 변환할 수 있습니다.  

[excel2markdown](https://tabletomarkdown.com/convert-spreadsheet-to-markdown/)  

![excel2markdown](/assets/images/tips/excel2markdown.jpg)  

```
| a  | b | a%b | (a-1)%b+1 | (a-1)/b+1 |
| -- | - | --- | --------- | --------- |
| 1  | 3 | 1   | 1         | 1         |
| 2  | 3 | 2   | 2         | 1         |
| 3  | 3 | 0   | 3         | 1         |
| 4  | 3 | 1   | 1         | 2         |
| 5  | 3 | 2   | 2         | 2         |
| 6  | 3 | 0   | 3         | 2         |
| 7  | 3 | 1   | 1         | 3         |
| 8  | 3 | 2   | 2         | 3         |
| 9  | 3 | 0   | 3         | 3         |
| 10 | 3 | 1   | 1         | 4         |
| 11 | 3 | 2   | 2         | 4         |
| 12 | 3 | 0   | 3         | 4         |
```

| a  | b | a%b | (a-1)%b+1 | (a-1)/b+1 |
| -- | - | --- | --------- | --------- |
| 1  | 3 | 1   | 1         | 1         |
| 2  | 3 | 2   | 2         | 1         |
| 3  | 3 | 0   | 3         | 1         |
| 4  | 3 | 1   | 1         | 2         |
| 5  | 3 | 2   | 2         | 2         |
| 6  | 3 | 0   | 3         | 2         |
| 7  | 3 | 1   | 1         | 3         |
| 8  | 3 | 2   | 2         | 3         |
| 9  | 3 | 0   | 3         | 3         |
| 10 | 3 | 1   | 1         | 4         |
| 11 | 3 | 2   | 2         | 4         |
| 12 | 3 | 0   | 3         | 4         |

**Success Notice:**  
미리 만들어놔주셔서 감사합니다! :+1: 
{: .notice--success}
 
