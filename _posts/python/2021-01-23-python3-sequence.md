---
title: "[Python] PS Python으로 시작할 때 알아야할 사항들"
excerpt: "입력, 빠른 입력, 정렬, 배열 생성 등"
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

## 시퀀스에 덧셈과 곱셈 연산자 사용하기

파이썬의 시퀀스는 +와 \*를 지원합니다. 일반적으로 덧셈의 경우 피연산자 두 개가 같은 자료형이어야 합니다. 둘 다 변경되지 않고 동일한 자료형의 시퀀스가 새로 만들어집니다.

\*는 하나의 시퀀스를 여러번 연결할 때 사용합니다. 정수를 곱해서 표현하면 새로운 시퀀스가 생성됩니다.

```
a = [1, 2, 3]
b = [4, 5, 6]
print(a + b)  # [1, 2, 3, 4, 5, 6]
print(a * 3)  # [1, 2, 3, 1, 2, 3, 1, 2, 3]
```

## 리스트의 리스트 만들기

정사각형의 게임판을 표현하는 경우 내포된 리스트를 초기화해야 하는 경우가 있습니다. 아래는 올바른 방법과 잘못도니 방법을 보여줍니다. 

```python
# 올바른 코드 ( 변경 사항이 1번만 적용 )
board = [['_'] * 3 for i in range(3)]
print(board)  # [['_', '_', '_'], ['_', '_', '_'], ['_', '_', '_']]
board[1][2] = '*'
print(board)  # [['_', '_', '_'], ['_', '_', '*'], ['_', '_', '_']]

# 잘못된 코드 ( 변경 사항이 3번 적용)
weird_board = [['_'] * 3] * 3
print(weird_board)  # [['_', '_', '_'], ['_', '_', '_'], ['_', '_', '_']]
weird_board[1][2] = '*'
print(weird_board)  # [['_', '_', '*'], ['_', '_', '*'], ['_', '_', '*']]
```

잘못된 코드가 잘못된 이유는 본질적으로 아래의 코드와 같기 때문입니다.

```python
# 올바른 코드의 동작 과정
board = []
for i in range(3):
    row = ['_'] * 3
    board.append(row)

# 잘못된 코드의 동작 과정
row = ['_'] * 3
board = []
for i in range(3):
    board.append(row)
```

기억할 점은 두 가지 입니다.

1. ['_'] * N을 해도 된다. 
1. ['_'] * N을 저장해두고 같은 값을 여러번 append하는 것이 안된다.  


# Reference

- <https://docs.python.org/ko/3/howto/sorting.html>

**Success Notice:**
수고하셨습니다. :+1:
{: .notice--success}