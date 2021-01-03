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

$(a+b) % c + 1$의 경우 연산자 우선순위를 모르면 $((a+b) % c) + 1$와 같이 불필요하게 괄호를 사용해야 합니다. 

**Success Notice:**  
+,-보다 * /가 연산자 우선순위가 높습니다.  
%는 *와 /와 연산자 우선순이가 같습니다.  
{: .notice--success}
 
