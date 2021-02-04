---
title: "[Python] 쉽게 정리한 입력"
excerpt: "input(), sys.stdin.read(), sys.stdin.readline()"
date: 2021-01-23
last_modified_at: 2021-01-28
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

# Input

1. `input()` : 
  - 한 줄을 읽는다
  - 개행문자를 제외한다
  - string으로 변환한다
  - EOF을 읽으면 EOFError를 raise한다.
1. `sys.stdin.readline()` : 
  - 한 줄을 읽는다.
  - 개행문자가 string 끝에 남는다.
  - 파일 마지막이 개행문자로 끝나지 않는 경우만 string으로 끝나지 않는다. 
  - readline()이 empty string을 return하는 것은 EOF에 도달했다는 것이다.

파일 입력이 개행문자 없는 '1'뿐이라면, 아래 처음의 input()이 파일을 읽으면 파일 전체가 읽어진다. 개행문자가 입력받지 않았기 때문에 제외할 개행문자가 없다. 이 상태에서 다시 input()을 수행하면 EOF를 읽고 EOFError를 raise한다.  

아래 코드처럼 input()을 한 번만 수행한 뒤, sys.stdin.readline()을 수행하면 EOF를 읽게된다. 따라서 arr에는 empty string이 들어가고 True가 출력된다.  

만약 파일 입력이 '1\n'였으면 input()에서 개행문자까지 모두 읽고 개행문자를 버린 뒤, sys.stdin.readline()은 EOF를 읽고 True를 출력한다.  

```python
import sys
from math import pi, sqrt
from collections import deque, Counter
from operator import itemgetter

sys.stdin = open('input.txt', 'r')

n = int(input())
for _ in range(n):
    arr = sys.stdin.readline()
    if arr == '':
        print(True, end='')

'''
/usr/bin/python3.8 /home/niklasjang/PycharmProjects/ps/main.py
True
Process finished with exit code 0
'''
```

1. `sys.stdin.read()` 
  - read(n)에 인자가 전달되지 않았다면 파일 전체를 읽는다.
  - 파일 전체를 읽은 뒤 다시 read()를 하면 readline()과 마찬가지로 empty string이 return된다.

# split()

string.split(sep, maxsplit)  

sep을 구분자 문자열로 사용해서 문자열에 있는 단어들의 리스트를 리턴합니다. maxsplit이 주어지면 최대 maxsplit번 분할이 수행되고 리스트에는 maxsplit+1개의 요소가 들어갑니다.  

```python
>>> '1,2,3'.split(',')
['1', '2', '3']
>>> '1,2,3'.split(',', maxsplit=1)
['1', '2,3']
>>> '1,2,,3,'.split(',')
['1', '2', '', '3', '']
```  

sep을 지정하지 않으면 앞뒤중간의 공백문자를 모두 무시하고 나머지 값을 리턴합니다. 공백문자에 대해서 sep을 지정하지 않고 나누면 []를 리턴합니다.  

# splitlines([keepends])

keepends가 True로 주어지지 않는 한, 결과 리스트에 줄 바꿈문자는 포함되지 않습니다. \n, \r, \r\n 등을 기준으로 나누고 list를 리턴합니다.  

파일 입력이 '3\na\nb\nc\n`을 입력받을 때 아래는 ['a', 'b', 'c', '']를 리턴합니다.  

```python
import sys


sys.stdin = open('input.txt', 'r')

n = int(input())
arr = sys.stdin.read().splitlines()
print(arr)
```

파일 입력의 마지막에 \n을 지운 3\na\nb\nc`을 입력받아야 ['a', 'b', 'c']를 리턴합니다.  

# Reference

- <https://docs.python.org/ko/3/howto/sorting.html>

**Success Notice:**
수고하셨습니다. :+1:
{: .notice--success}