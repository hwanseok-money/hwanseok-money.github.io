---
title: "[인턴쉽] NAVER 동영상기술1개발팀 백엔드 인턴"
excerpt: "2020.01.06 ~ 2020.02.28"
date: 2021-01-30
last_modified_at: 
categories:
  - Project
tags:
  - Project 
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

## 요약
- 2020.01.06 ~ 2020.02.28
- 동영상기술1개발팀, 백엔드 인턴
- RTMP Relay Server 개발
- c++, socket programming, multi thread, git, RTMP, FLV, AMF3, ubuntu18.04
- [인턴 수료 증명서](/assets/images/about/certification_internship_naver.pdf)

## RTMP Relay Server

### 진행기간	
2020-01-06 ~ 2020-02-29  

### 주요내용  

미디어 서버의 공인 IP 할당 비용 감소를 위한 Proxy Server를 설계 및 개발했습니다. RTMP Relay server는 multimedia publisher로부터 데이터를 받아서 media server로 relay하는 proxy server의 역할을 수행합니다. 가장 기본적인 stream은 publisher와 media server 각각에 대한 세션을 하나씩 가집니다. 이와 같은 경우를 1 대 1 stream이라고 할 때, 서버는 N개의 1 대 M 스트림을 관리해야 합니다. 한 명의 publisher가 M 개의 media server로 패킷을 보내고,와.같은 stream을 N개 관리할 수 있어야 합니다.

### 새로운 분야  

c++ 기반 멀티 쓰레드 구조의 서버를 직접 설계했습니다. 서버 설계에 대한 경험이 없었지만, 기존의 RTMP Relay Server는 다양한 요구사항에 대응하는데 한계가 있었기 때문에 변화가 필요했습니다.  설계 뿐만 아니라 Protocol 기반의 개발과 서버의 성능 측정 부분도 낯분.였습니다. 

### 설계  

설계 단계에서는 크게 다섯 가지의 요구사항을 고려하였습니다. 첫째, 하나의 stream에서 사용하는 메모리가 증가하여도 다른 stream에는 영향을 주지 않아야 합니다. 둘째, 각 stream에 대해서 잠시 session이 중단되었다가 재 접속되어도 기존의 stream을 사용할 수 있어야 합니다. 셋째, packet의 일부가 drop되는 경우에도 media server가 이해할 수 있는 포맷으로 변경해서 보내주어야 합니다. 넷째, 추가적인 API 요청이 들어와도 기존의 stream에 영향을 주지 않고 응답해야 합니다. 다섯째, publisher와의 연결이 중단된 경우 같은 stream에 포함된 모든 media server와의 세션이 안전하게 종료되어야 합니다. 이를 위해서 TCP 세션 생성과 RTMP read의 네트워크 아키텍처로 epoll을 선택했고, 각 event에 대한 응답은 서로 다른 thread에서 수행하도록 구성했습니다.

### 개발  

개발 단계에서의 크게 세 가지에 집중했습니다. 먼저, thread를 원하는 시점에 멈출 수 있도록 Stoppable Thread Class를 도입하였습니다. thread의 유연한 관리는 다양한 요구사항을 반영하기에 필수 조건이라고 생각했기 때문입니다. 다음으로, RTMP, FLV, AMF3의 specification 문서를 통해 파악한 Data Format을 오차없이 구현했습니다. 전체의 흐름 속에서 꼭 필요한 부분을 집중적으로 이해함으로써 개발기간을 단축하고자 노력했습니다. 마지막으로 Smart Pointer를 이용한 Shared Memory를 사용하였습니다. 1 대 M Relay에서 하나의 패킷을 relay하기 위해 M번의 memcpy가 발생하여 memory 사용량이 폭증하는 문제가 있었습니다. 저는 shared_ptr를 사용하여 메모리 복사의 횟수를 줄이는 방법을 적용하여 해결하였습니다.

### 성능 측정  

성능 측정 단계는 2Mbps의 네트워크 대역폭을 가지는 환경에서 CPU 사용량, memory 사용량, relay delay를 기준으로 진행되었습니다. 1대 1 relay에서는 RTMP Relay Server 내부에서 20ms의 delay가 측정되었습니다. 하지만 100개의 1 대 2 relay stream을 관리할 때에는 약 300ms까지 delay가 증가하는 문제가 발생했습니다. 

### 원인 분석  

한정된 수의 Thread를 생성하고 사용할 수 있도록 Thread Pool을 적용하지 못한 점이 원인입니다. Publisher의 요청이 추가될 때마다 M개의 Thread를 생성하기 때문에, Context Switching 비용이 크게 증가함에 따라 delay가 늘어난 것으로 파악되었습니다. 

## 데모영상  

https://youtu.be/HRnQ_yF2EOc?t=16

## Skill 또는 지식  

C++11, Multi Thread, RTMP, FLV, AMF3, ubuntu18.04

**Success Notice:**  
감사합니다! :+1:
{: .notice--success}