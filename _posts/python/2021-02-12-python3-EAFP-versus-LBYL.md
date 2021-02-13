---
title: "[Python] EAFP versus LBYL"
excerpt: ""
date: 2021-02-12
last_modified_at: 
categories:
  - Python
tags:
  - Python
  - EAFP 
  - LBYL
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

# EAFP versus LBYL

- EAFP
    - 'It's Easier to Ask Forgiveness than Permission' 의 줄임말 입니다. 
    - 허락보다 용서구하는 것이 쉽다.

- LBYL
    - 'Look Before You Leap'의 줄임말입니다. 
    - 도약하기전에 봐라. 라는 뜻입니다.

# EAFP를 지향하되, EAFP가 불편한 경우 LBYL를 사용하자

## EAFP를 지향하는 경우

```python
# EAFP
try:
    do_something(dict_["key"])
except KeyError:
    pass
```

```python
# LBYL
try:
    value += dict_["key"]
except KeyError:
    pass
```

## EAFP가 불편한 경우 

The problem with that code, though, is what happens if do_something() throws a KeyError itself that you didn’t want suppressed?  

아래와 같은 경우 LBYL를 사용하는 것이 더 좋습니다.  

1. 코드를 locl scope에서 localize하고 싶은 경우
2. EAFP seems overly explicit해보이는 경우  

```python
# EAFP
try:
    value = dict_["key"]
except KeyError:
    pass
else:
    do_something(value)
```

```python
# LBYL
if "key" in dict_:
    do_something(dict["key"])
```

# except로 인한 EAFP의 성능

except로 인한 성능 저하를 걱정하지 않아도 됩니다.  

If you are coming to Python from a programming language where exceptions are an expensive thing to trigger then that worry would be understandable. But since exceptions are used for control flow like in EAFP, Python implementations work hard to make exceptions a cheap operation, and so you should not worry about the cost of exceptions when writing your code.  

# Reference

- [EAFP - 허락보다 용서구하는 것이 쉽다.](https://wikidocs.net/16062)
- [Idiomatic Python: EAFP versus LBYL](https://devblogs.microsoft.com/python/idiomatic-python-eafp-versus-lbyl/)  

**Success Notice:**
수고하셨습니다. :+1:
{: .notice--success}