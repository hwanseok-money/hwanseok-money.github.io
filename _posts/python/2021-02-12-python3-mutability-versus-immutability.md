---
title: "[Python] Mutability and Immutability"
excerpt: ""
date: 2021-02-12
last_modified_at: 
categories:
  - Python
tags:
  - Python
  - Mutability 
  - Immutability
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

# id()

Id is a built-in function in Python. It gives us the ability to check the unique identifier of an object. The unique identifier is pointing to a location in memory, which is an object.  

```python
>>> a=1
>>> b=2
>>> c=2
>>> id(a) # 1987543152Python keeps an array of integer objects for all integers between -5 and 256
>>> id(b) # 1987543184
>>> id(c) # 1987543184
>>> a='str'
>>> b='str'
>>> id(a) # 2240228419488
>>> id(b) # 2240228419488
>>> id(a)==id(b) # True

'''
Python keeps an array of integer objects for all integers between -5 and 256
with NSMALLNEGINTS, NSMALLPOSINTS
'''
>>> a=260
>>> b=260
>>> id(a) # 2240228470512
>>> id(b) # 2240259876400
>>> id(a)==id(b) # False
```

# aliased, cloned

```python
# aliased
>>> list1 = [1, 2, 3]
>>> list2 = list1
>>> list1 is list2
True
```  

```
# cloned
>>> list1 = [1, 2, 3]
>>> list2 = list1[:]
>>> list1
[1, 2, 3]
>>> list2
[1, 2, 3]
>>> list1 is list2
False
>>> id(list1) == id(list2)
False
```

# type

An object has three things: id, type, and value. EVEN METHOD.

```python
>>> type([2, 3, 4])
<class 'list'>
>>> type({'category': 'produce', 'count': 200})
<class 'dict'>
>>> type(print)
<class 'builtin_function_or_method'>
>>> type(type)
<class 'type'>
```

# Mutable : List, Dict, Set

A mutable object is a changeable object and its state can be modified after it is created. If we want to change the first value in our list and print it out, we can see that the list changed, but the memory address of the list is the same. It changed the value in place. That’s what mutable means.  

```python
lst = [1,2,3]
prev = id(lst)
lst[0] = 10
curr = id(lst)
prev == curr # true
id(lst) == id(lst[0]) # false
```

```python
>>> lst = [1000, 2000, 3000]
>>> id(lst) # 2240261230344
>>> id(lst[0]) # 2240259876048
>>> lst.append(4)
>>> id(lst) # 2240261230344 append 전과 같은 객체
>>> id(lst[0]) # 2240259876048
>>> id(lst[3]) # 1987543248
```

# Immutable : integer, float, string, tuple, bool, frozenset

- 객체 내부의 값을 index로 지정해서 수정할 수 없음
- 값을 변경하고 싶으면 새로운 객체가 생성되고, 변수가 참조하게 됨

# Mutability and Immutability의 중요성  

Immutability may be used to ensure that an object remains constant throughout your program. The values of mutable objects can be changed at any time and place, whether you expect it or not.

# 함수 파라미터에서의 활용

```python
# integer : Immutability
def increment(n):
    n += 1

b = 9
increment(b)
print(b)
```

```python
# list : Mutability
# my_list is changed
def increment(n):
    n.append(4)

my_list = [1, 2, 3]
increment(my_list)
print(my_list) # [1,2,3,4]
```

```python
# list : Mutability
# my_list is not changed
def my_func(working_list=None):
    if working_list is None: 
        working_list = []

    working_list.append("a")
    print(working_list)
```

# Reference

- [Mutability and Immutability in Python](https://medium.com/datadriveninvestor/mutable-and-immutable-python-2093deeac8d9)  

**Success Notice:**
수고하셨습니다. :+1:
{: .notice--success}