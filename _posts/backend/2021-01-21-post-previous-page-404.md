---
title: "[Django] 정렬 및 필터링은 get으르 사용해야 하는 이유"
excerpt: "가변 (키워드)인자의 사용법"
date: 2021-01-21
last_modified_at: 
categories:
  - Backend
tags:
  - Backend
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

**Info Notice:**  
안녕하세요. **HwanSeok**입니다.  
본 포스팅은 backend의 기초 개념을 다지는 포스팅입니다.  
{: .notice--info}


## ???


kw를 POST 방식으로 전달하는 방법은 추천하지 않는다. 왜냐하면 kw를 POST 방식으로 전달하면 page 역시 POST 방식으로 전달해야 하기 때문이다. 또한 POST 방식으로 검색, 페이징 기능을 만들면 웹 브라우저에서 '새로고침' 또는 '뒤로가기'를 했을 때 '만료된 페이지' 오류를 종종 만나게 된다. POST 방식은 동일한 POST 요청이 발생하면 중복을 방지하려고 오류를 발생시키기 때문이다.

예를 들어 2페이지에서 3페이지로 갔다가 '뒤로가기'를 하여 2페이지로 갈 때 '만료된 페이지' 오류를 만날 수 있다. 이러한 이유로 게시판을 조회하는 목록 함수는 GET 방식을 사용해야 한다. 이후 알아볼 정렬 기능 역시 GET 방식으로 구현할 것이다. 그러면 본격적으로 검색 기능을 만들어 보자.

## Reference

- [args-and-kwargs][2]

**Success Notice:**  
수고하셨습니다. :+1:
{: .notice--success}

[1]: https://docs.djangoproject.com/ko/3.1/ref/urlresolvers/#reverse
[2]: https://www.programiz.com/python-programming/args-and-kwargs