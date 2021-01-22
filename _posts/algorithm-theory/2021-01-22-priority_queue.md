---
title: "[이론] 우선순위 큐 Priority Queue "
excerpt: ""
date: 2021-01-22
last_modified_at:
categories:
  - Algorithm-Theory
tags:
  - Algorithm-Theory
  - Practice
  - priority-queue
  - 우선순위 큐
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

# 우선순위 큐

## Heap

우선순위 큐를 구현하기 위해 사용하는 자료구조 중 하나입니다. `최소 힙`과 `최대 힙`이 있습니다.  

|우선순위 큐 구현 방식| 삽입 | 삭제 |
|:------------------|:------|:----|
|list | O(1) | O(N) |
|Heap | O(logN) | O(logN) |

## Sort with min heap

```python
import heapq


def heapsort(iterable):
    h = []
    result = []
    for value in iterable:
        heapq.heappush(h, value)
    for i in range(len(h)):
        result.append(heapq.heappop(h))
    return result


result = heapsort([1, 3, 5, 7, 9, 2, 4, 6, 8, 0])
print(result) # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```  



**Success Notice:**
수고하셨습니다. :+1:
{: .notice--success}