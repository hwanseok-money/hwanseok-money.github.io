---
title: "[Tips] (a-1)%b+1 사용하기"
excerpt: ""
date: 2021-01-04
categories:
  - Tips
tags:
  - Tips
  - 연산자
  - 우선순위
  - operator
  - priority
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true

---

## 문제 상황

아래 표에 있는 식은 외워두면 좋습니다. 

- $(a-1)%b+1$ : 1, ... , b를 반복해서 얻을 수 있음
- $(a-1)/b+1$ : 1 b개, 2 b개 ...를 반복해서 얻을 수 있음

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

아래와 같은 문제에서 사용될 수 있습니다.  

- [ACM호텔](https://hwanseok-dev.github.io/algorithm/boj-impl-10250/)
- [분산처리](https://hwanseok-dev.github.io/algorithm/boj-impl-1009/)

**Success Notice:**
수고하셨습니다. :+1:
{: .notice--success}
 
