---
title: "[Backend] 소켓 통신과 HTTP 통신"
excerpt: ""
date: 2021-02-15
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

# 소켓 통신

접속을 계속 유지하여, 데이터를 전달합니다. 서버의 자원에 따라서 연결될 수 있는 클라이언트의 숫자가 한정됩니다. 실시간 정보 교환에 사용하며 HTTP보다 속도가 빠릅니다.  

# HTTP 통신

클라이언트의 요청이 있을 때만 데이터 응답을 전달합니다. 불필요한 자원의 점유를 없애 다른 접속을 원활하게 처리할 수 있습니다. 데이터 요청 후 응답이오면 연결을 끊어집니다.  

# Reference

- 