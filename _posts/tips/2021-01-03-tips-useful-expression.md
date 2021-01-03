---
title: "[Tips] 나누기 연산자 우선순위"
excerpt: ""
date: 2021-01-03
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

**Success Notice:**  
+,-보다 * /가 연산자 우선순위가 높습니다.  
%는 *와 /와 연산자 우선순이가 같습니다.  
{: .notice--success}
 
