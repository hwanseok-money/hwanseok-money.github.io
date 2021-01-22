---
title: "[이론] 이분탐색 "
excerpt: ""
date: 2021-01-22
last_modified_at:
categories:
  - Algorithm-Theory
tags:
  - Algorithm-Theory
  - Practice
  - binary-search
  - 이분탐색
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

# 이분탐색

## 직접 구현(중복된 값이 없는 경우)

```python
def binary_search(arr, target, start, end):
    if start > end:
        return None
    mid = (start + end) // 2
    if arr[mid] == target:
        return mid
    elif arr[mid] > target:
        return binary_search(arr, target, start, mid - 1)
    else:
        return binary_search(arr, target, mid + 1, end)


n = 10
target = 7
arr = [1, 3, 6, 7, 9, 2, 4, 5, 9, 1]
arr.sort()
print(arr)
result = binary_search(arr, target, 0, n - 1)
if result is None:
    print("원소가 존재하지 않습니다.")
else:
    print(result + 1)
```

## 라이브러리 bisect

c++의 lower_bound, upper_bound로 생각하면 됩니다.  

```python
from bisect import bisect_left, bisect_right

#      0  1  2  3  4  5  6  7  8  9
arr = [1, 1, 2, 3, 4, 5, 7, 7, 9, 9]
target = 7
print(bisect_left(arr, target))  # 6
print(bisect_right(arr, target))  # 8
print(bisect_right(arr, target) - bisect_left(arr, target))  # 2
```


**Success Notice:**
수고하셨습니다. :+1:
{: .notice--success}