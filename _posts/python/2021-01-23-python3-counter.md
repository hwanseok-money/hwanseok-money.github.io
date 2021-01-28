---
title: "[Python] 각 요소가 등장하는 횟수 쉽게 구하기"
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
>>> from collections import Counter
>>> Counter('abracadabra').most_common(3)
[('a', 5), ('b', 2), ('r', 2)]
>>> Counter('abracadabra').most_common()
[('a', 5), ('b', 2), ('r', 2), ('c', 1), ('d', 1)]
```  



# Reference

- <https://docs.python.org/3/library/collections.html#collections.Counter>

**Success Notice:**
수고하셨습니다. :+1:
{: .notice--success}