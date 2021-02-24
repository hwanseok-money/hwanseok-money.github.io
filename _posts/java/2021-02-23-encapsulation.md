---
title: "[Java] 캡슐화"
excerpt: "Encapsulation"
date: 2021-02-23
categories:
  - Java
tags:
  - java
  - 캡슐화
  - Encapsulation
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
classes: wide
---

## 캡슐화

객체 지향을 기본적으로 캡슐화를 진행한다.  
캡슐화는 내부 기능 구현이 변경되어도, 그 기능을 사용하는 코드는 영향을 받지 않도록 한다.  

다른 클래스의 데이터를 다루려면 메소드를 통해야 한다. 멤버변수를 private로 설정해서 접근제한 시키고 메서드를 통해서 접근하도록 한다.  