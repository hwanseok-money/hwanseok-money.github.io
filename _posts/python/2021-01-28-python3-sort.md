---
title: "[Python] 쉽게 정리한 정렬"
excerpt: ""
date: 2021-01-28
last_modified_at: 
categories:
  - Python
tags:
  - Python
  - IO
  - FastIO
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

# 정렬

## 기본 오름차순 정렬 

arr = [1,4,3,5,2]라고 할 때,  

- 오름차순 정렬 : sorted(arr)
  - arr은 변경되지 않음
  - 모든 iterable 가능.
- 오름차순 정렬 : arr.sort()
  - arr이 변경됨
  - list만 가능

## 키 함수를 사용한 정렬

문자열에 대해서 split()을 하면 단어를 기준으로 string list가 생성됩니다. key함수는 iterable한 객체의 입력 레코드에 정확히 한 번씩 호출됩니다. 이 함수가 적용된 결과를 기준으로 정렬이 이루어집니다.  

아래의 예시는 대소문자 상관없이 앞에 오는 문자의 ascii를 기준으로 정렬합니다.  

```python
sorted("This is a test string from Andrew".split(), key=str.lower)
['a', 'Andrew', 'from', 'is', 'string', 'test', 'This']
```  

## 키 함수=람다를 사용한 정렬

```python
student_tuples = [
    # name, grade, age
    ('john', 'A', 15),
    ('jane', 'B', 12),
    ('dave', 'B', 10),
]
sorted(student_tuples, key=lambda x: x[2])   # sort by age
# [('dave', 'B', 10), ('jane', 'B', 12), ('john', 'A', 15)]
```   

## 키 함수=itemgetter를 사용한 정렬

위와 같이 람다를 매우 일반적인 방법으로 쓰는 경우 itemgetter를 사용할 수 있습니다. key=lambda x:x[2]와 itemgetter(2)는 동일합니다. x가 class인 경우 attrgetter를 사용할 수 있습니다. operator 모듈 함수는 다중 수준의 정렬을 허용합니다. 예를 들어, 먼저 grade로 정렬한 다음 age로 정렬하려면, 이렇게 합니다  

```python
from operator import itemgetter, attrgetter
student_objects = [
    Student('john', 'A', 15),
    Student('jane', 'B', 12),
    Student('dave', 'B', 10),
]
sorted(student_tuples, key=itemgetter(2))
#[('dave', 'B', 10), ('jane', 'B', 12), ('john', 'A', 15)]
sorted(student_objects, key=attrgetter('age'))
#[('dave', 'B', 10), ('jane', 'B', 12), ('john', 'A', 15)]
sorted(student_tuples, key=itemgetter(1,2))
#[('john', 'A', 15), ('dave', 'B', 10), ('jane', 'B', 12)]
sorted(student_objects, key=attrgetter('grade', 'age'))
# [('john', 'A', 15), ('dave', 'B', 10), ('jane', 'B', 12)]
```

## stable sort 

3개의 나이와 이름을 입력받아  

```python
# input
3
21 Junkyu
21 Dohyun
20 Sunyoung
```

나이로 정렬하되, 나이가 같은 경우 이름을 입력받은 그대로 두는 stable sort의 경우는 (나이, 입력받은 순서)가 key가 됩니다. 따라서 아래와 같이 정렬을 해야하는 iterable에 입력받은 순서(i)를 포함시켜서 적절한 key순서로 지정해줍니다.  

```python
for i, v in enumerate(arr):
    ans.append([i, int(v[0]), v[1]])
# ans = sorted(ans, key=lambda x:(x[1], x[0]))
ans = sorted(ans, key=itemgetter(1, 0))
for i in ans:
    print(i[1], i[2])
```  

```python
# output
20 Sunyoung
21 Junkyu
21 Dohyun
```

그런데 사실 python의 정렬은 stable을 지원하기 때문에 입력받은 순서를 key로 지정하지 않아도 됩니다. 

```python
import sys
from math import pi, sqrt
from collections import deque, Counter
from operator import itemgetter

# sys.stdin = open('input.txt', 'r')

n = int(input())
arr = [input().split() for _ in range(n)]
ans = []
for i, v in enumerate(arr):
    ans.append([int(v[0]), v[1]])
ans = sorted(ans, key=itemgetter(0))
for i in ans:
    print(i[0], i[1])
```

## stable sort이기 때문에 

stable이기 때문에 key(A,B)에 대해서 A를 내림차순으로 정렬하되, A가 같은 경우 B를 오름차순으로 정렬하기 위해서는 아래와 같이 수행해도 됩니다.  

1. B를 먼저 오름차순으로 정렬하기
1. A를 내림차순으로 또 정렬하기

```python
s = sorted(student_objects, key=attrgetter('age'))     # sort on secondary key
sorted(s, key=attrgetter('grade'), reverse=True)       # now sort on primary key, descending
#[('dave', 'B', 10), ('jane', 'B', 12), ('john', 'A', 15)]
```

위 과정을 함수화하면 다음과 같은 모습입니다.  

```python
def multisort(xs, specs):
    for key, reverse in reversed(specs):
        xs.sort(key=attrgetter(key), reverse=reverse)
    return xs
>>>
multisort(list(student_objects), (('grade', True), ('age', False)))
[('dave', 'B', 10), ('jane', 'B', 12), ('john', 'A', 15)]
```

## cmp를 사용하는 방법은 지양합시다

cmp를 사용하는 낡은 방법은 key를 사용하는 방법으로 대체해서 사용합니다!  

```python
def numeric_compare(x, y):
    return x - y
sorted([5, 2, 4, 1, 3], cmp=numeric_compare) 
[1, 2, 3, 4, 5]
```


# Reference

- <https://docs.python.org/ko/3/howto/sorting.html>

**Success Notice:**
수고하셨습니다. :+1:
{: .notice--success}