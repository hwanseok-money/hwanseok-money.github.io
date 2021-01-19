---
title: "[Django][The Polls][Chap 7] 추가적인 기능 구현"
excerpt: "업그레이드!"
date: 2021-01-17
last_modified_at: 
categories:
  - Django
tags:
  - Django
  - The Polls
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: false
---

**Info Notice:**  
안녕하세요. **HwanSeok**입니다.  
본 포스팅은 django의 기초 개념을 다지는 포스팅입니다.  
{: .notice--info}

## null v.s. blank

- `null` : If True, Django will store empty values as NULL in the database. Default is False
  -  null is purely database-related
- `blank` : If True, the field is allowed to be blank. Default is False. 
  -  blank is validation-related
  -  If a field has blank=True, form validation will allow entry of an empty value. If a field has blank=False, the field will be required.  

**Success Notice:**
위와 같은 과정을 거쳐 처음에 보았던 결과 페이지를 생성하였습니다. 수고하셨습니다. :+1:
{: .notice--success}
