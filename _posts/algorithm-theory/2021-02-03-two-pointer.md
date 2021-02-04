---
title: "[이론] 투 포인터"
excerpt: ""
date: 2021-02-03
last_modified_at:
categories:
  - Algorithm-Practice
tags:
  - Algorithm-Practice
  - Practice
  - 투 포인터
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

## 알고리즘 설명

투 포인터 알고리즘을 사용할 수 있는 전형적인 문제들이 있습니다. 배열의 시작점에 left, right를 설정해두고, 특정 조건을 만족할 때 right를 +1 하거나 left를 +1합니다. 동시에 arr[left:right+1]의 범위가 문제의 정답 조건과  같은지 비교를 합니다. left<=right라는 조건을 만족하면서 진행되기 때문에, 그리고 left와 right가 -1되는 겨우는 없기 때문에 $O(n)+O(n) = O(n)$의 시간복잡도를 가집니다.  

백준의 투 포인터 기본 문제를 통해 알아보겠습니다.  

## 문제 링크

[문제링크](https://www.acmicpc.net/problem/2003)  

## 첫 번째 풀이 

### 정답 코드

부분합이 m이 되는 구간의 갯수를 찾는 문제입니다. left와 right는 0으로 시작합니다. s = [left,right]의 합입니다.  

1. s == m 일때는 ans += 1, right += 1  
2. s < m 일 때는 right += 1, s+= arr[right]
3. s > m 일 때는 s -= arr[left], left += 1

[항공대 알고리즘 소학회](https://kau-algorithm.tistory.com/119) 천수환님의 투 포인터 강의는 [여기](https://www.youtube.com/watch?v=L5Aoq447YWM)에서 확인하실 수 있습니다 ^^7  

```python
import sys
from math import sqrt, ceil
from bisect import bisect_left, bisect_right
from operator import itemgetter

# sys.stdin = open("input.txt", "r")
# dp = [[[0] * K for _ in range(C)] for _ in range(R)]
# MOD = 1000000000
n, k = map(int, sys.stdin.readline().split())
arr = list(map(int, sys.stdin.readline().split()))
left, right = 0, 0

s = arr[0]
ans = 0
while True:
    if s == k:
        ans += 1
        right += 1
        if right == n:
            break
        s += arr[right]
    elif s < k:
        right += 1
        if right == n:
            break
        s += arr[right]
    else:
        s -= arr[left]
        left += 1

print(ans)
```

**Success Notice:**
수고하셨습니다. :+1:
{: .notice--success}