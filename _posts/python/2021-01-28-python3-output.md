---
title: "[Python] 다양한 출력 방법"
excerpt: "print의 형식 지정 세 가지 방법"
date: 2021-01-23
last_modified_at: 2021-01-28
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

# Ouput

## 첫 번째 방법 format

```python
a, b, = 1, 2

# 키워드 지정
print('a is {a} and b is {b}'.format(a=2, b=3))
# 인덱스 미지정
print('a is {} and b is {}'.format(a, b))
# 인덱스 정방향
print('a is {0} and b is {1}'.format(a, b))
# 인덱스 직접 지정
print('a is {1} and b is {0}'.format(a, b))
'''
a is 2 and b is 3
a is 1 and b is 2
a is 1 and b is 2
a is 2 and b is 1
'''
```  

```python
# {} 출력하는 법
print('How to print {}')
print('How to print \{\{\}\}')
print('How to print \{\{\}\} {}'.format('test'))
'''
How to print {}
How to print \{\{\}\}
How to print {} test
'''
```

```python
# 자릿수 출력은 kw 또는 인덱스 필수
a = 1.23456789
b = 9.87654321
# 키워드 자릿수 지정
print('a is {a:0.1f} and b is {b:0.4f}'.format(a=2, b=3))
# 인덱스 직접 지정
print('a is {0:0.5f} and b is {1:0.7f}'.format(1.23456789, 9.87654321))

'''
a is 2.0 and b is 3.0000
a is 1.23457 and b is 9.8765432
'''
```  

## 두 번째 방법 %

```python
print('int is %d\nflout is %f\nstring is %s\n'
      % (123, 123.456, 'here'))
```

## 세 번째 방법 f-string

```python
s = 'hwanseok'
n = 5
format = f'I am {s} and I like {n}'
print(format)
# I am hwanseok and I like 5
```

# Reference

- <https://docs.python.org/ko/3/howto/sorting.html>

**Success Notice:**
수고하셨습니다. :+1:
{: .notice--success}