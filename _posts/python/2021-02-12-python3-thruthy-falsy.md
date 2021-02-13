---
title: "[Python] Thuthy and Falsy"
excerpt: ""
date: 2021-02-12
last_modified_at: 2021-02-13
categories:
  - Python
tags:
  - Python
  - Thuthy 
  - Falsy
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

# 파이썬에서의 Truthy Falsy

다른 강타입 언어들과 비교하여 파이썬이 갖는 재밌는 특징은, 어떤 타입의 오브젝트던 인스턴스 자체를 if문의 조건으로 사용할 수 있으며, 논리 연산의 피연산자로 사용할 수 있다는 것이다.  

```python
obj = AnyObject() # int, string, array, tuple, dict, class ...

# 이런 거라던가
if obj:
  pass

# 이런 것도 가능하다
ret = obj or obj2 and obj3
```   

이를 통하여 파이썬에서 임의의 오브젝트는 자신의 참/거짓을 정할 수 있게 된다. 이들은 논리 연산에서 True / False로 취급되지만, 엄밀한 True / False와는 구분 되어야 하므로, 참으로 취급 되는 값(Truthy), 거짓으로 취급되는 값(Falsy)라는 용어를 사용한다.  

# Falsy Values

Falsy Values는 7개뿐입니다.  

1. False
1. None
1. 0, 0.0, 0L, 0j
1. ""
1. []
1. ()
1. {}

# Truthy Values

Falsy Values 7개를 제외한 나머지는 모두 Thuthy합니다.  

주의할 점은 `음수`도 Truthy합니다.  

```python
if -1231231:
    print(True)
else :
    print(False)
# True
```

# Reference

- [파이썬에서의 Truthy Falsy](https://ryanking13.github.io/2018/04/05/python-truthy-falsey.html)  

**Success Notice:**
수고하셨습니다. :+1:
{: .notice--success}