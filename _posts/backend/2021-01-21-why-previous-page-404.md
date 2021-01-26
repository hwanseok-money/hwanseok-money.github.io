---
title: "[Back-end] 뒤로가기 버튼 클릭시 만료된 페이지가 뜨는 원인"
excerpt: "GET방식과 POST 방식의 차이"
date: 2021-01-21
last_modified_at: 2021-01-25 
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


## 만료된 페이지

뒤로가기 버튼을 눌렀을 때, 해당 페이지를 구성하는 정보 중에서 static하지 않은 정보가 있을 수 있습니다. 즉, 해당 페이지를 보여주기 위해서 API를 통해서 전달받은 데이터가 필요한 경우입니다. API를 통해서 받은 데이터를 모두 다 cache해두면 좋겠지만 브라우저의 보안 정책의 이유로 cache되지 못하는 상황이 발생합니다.  

바로 이 때 `만료된 문서`라는 페이지를 보게됩니다. 페이지를 띄워야해서 데이터가 필요한데, 필요한 데이터가 cache되어 있지 않습니다. 그려면 다시 API 요청을 보내야합니다. 그런데 만약 해당 페이지에 또 다른 데이터를 추가/수정하는 API Call이 포함된 경우 의도치 않은 동작이 발생할 수 있습니다. 이를 막기 위해서 브라우저에서 자체적으로 API 요청을 다시 날릴 것인지 확인하는 페이지를 띄우고 이게 `만료된 페이지`입니다.  

## POST를 사용할 때는 중복 요청에 대한 대비가 필요하다

위에서 언급한 의도치 않은 동작은 POST를 수행할 때의 이야기 입니다. 일반적으로 GET은 데이터를 조회할 때, POST는 수정, 삭제 할 때 사용합니다. 따라서 GET으로 데이터를 조회하는 것은 뒤로가기 버튼 눌러서 다시 수행되어도 큰 문제가 없습니다. POST가 꼭 필요해서 POST를 사용할 때에도, `만료된 문서`페이지를 볼 수 있기 때문에, **중복된 POST에 대한 처리**를 서비스에 맞게 잘 구현해야 합니다. keyword를 전달해서 이를 기반으로 sort를 하는 경우는 GET으로 수행하는 것이 바람직합니다.  

## Reference

-<https://blog.outsider.ne.kr/312>

**Success Notice:**  
수고하셨습니다. :+1:
{: .notice--success}