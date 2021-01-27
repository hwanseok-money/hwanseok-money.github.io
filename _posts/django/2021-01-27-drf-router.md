---
title: "[Django REST framework] 기본 Routers와 정규표현식 Url"
excerpt: "router 설정만으로 CRUD가 가능한 이유"
date: 2021-01-27
last_modified_at:
categories:
  - Django
tags:
  - Django
  - DjangoRestFramework
  - router
  - 정규표현식
  - regex
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: false
---

**Info Notice:**  
안녕하세요. **HwanSeok**입니다.  
{: .notice--info}

# Router를 적용한 소스코드 미리보기

아래 링크에서 router가 동작하는 소스코드 상태를 미리 확인할 수 있습니다. 

- 전체 프로젝트는  [여기][1]
- urls.py는 [여기][2]
- todo app은 [여기][3]

# 접속 가능한 경로

- model list view : http://localhost:8000/api/todos/  

![drf-0](/assets/images/django/drf-0.jpg)  

- model detail view : http://localhost:8000/api/todos/1/

![drf-1](/assets/images/django/drf-1.jpg)  


# url 경로에 r' '을 쓰는 이유

`raw python string literal`이라고 하여, '\n'을 포함한 space chracter를 문자열로 취급한다  


`raw python string literal`를 사용하지 않은 경우  

```python
s = "Hello\tfrom AskPython\nHi"
print(s)
'''
Hello    from AskPython
Hi
'''
```

`raw python string literal`를 사용한 경우  

```python
s = r"Hello\tfrom AskPython\nHi"
print(s)
'''
Hello\tfrom AskPython\nHi
'''
```  

'\x'의 경우 존재하지 않은 unicode이기 때문에 `raw python string literal`를 사용하지 않으면 에러가 난다.  

```python
s = "Hello\xfrom AskPython"
print(s) # SyntaxError
s = r"Hello\xfrom AskPython"
print(s) # Hello\xfrom AskPython
```  

# 원하는 패턴의 경로만을 입력받기 위한 정규표현식

![drf-2](/assets/images/django/drf-2.jpg)  

추가적인 방법은 [여기][4]에 나와있습니다.  





**Success Notice:**
{: .notice--success}

# 개발환경

- ubuntu 20.04
- python 3.8.5
- django 3.1.5
- pip 20.0.2
- yarn 1.22.10

[1]: https://github.com/hwanseok-dev/the-insta
[2]: https://github.com/hwanseok-dev/the-insta/blob/v1.0/config/urls.py
[3]: https://github.com/hwanseok-dev/the-insta/tree/v1.0/todo
[4]: https://simpleisbetterthancomplex.com/references/2016/10/10/url-patterns.html