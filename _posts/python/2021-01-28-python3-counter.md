---
title: "[Python] Counter, 각 요소가 등장하는 횟수 쉽게 구하기"
excerpt: "from collections import counter"
date: 2021-01-28
last_modified_at:
categories:
  - Python
tags:
  - Python
  - IO
  - FastIO
  - C++
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

# Counter

```python
'''
10
1 2 3 4 2 5 3 1 1 2
'''
import sys
from collections import Counter

sys.stdin = open("input.txt", "r")
n = int(input())
arr = list(map(int, sys.stdin.readline().split()))

counter = Counter(arr)  # list to Counter object
print(counter)  # Counter({1: 3, 2: 3, 3: 2, 4: 1, 5: 1})
counter_list = counter.most_common()  # 등장 횟수가 많은 순서대로 정렬 후 list로 return
print(counter_list)  # [(1, 3), (2, 3), (3, 2), (4, 1), (5, 1)]
for x in counter:
    print(x)  # 1 2 3 4 5
    print(x in counter)  # True True True True True
```  

# Reference

- <https://docs.python.org/3/library/collections.html#collections.Counter>

**Success Notice:**
수고하셨습니다. :+1:
{: .notice--success}