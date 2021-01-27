---
title: "[Backend] ACID(Atomicity Consistency Isolation Durability)와 CRUD(Create Read Update Delete)"
excerpt: "데이터베이스 기본"
date: 2021-01-25
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

# 트랜잭션

트랜잭션은 데이터베이스의 상태를 변화시키는 하나의 논리적인 기능을 수행하기 위한 작업의 단위(한 번에 수행되어야 하는 일련의 연산)입니다.  

# ACID

데이터의 무결성Integrity를 보장하기 위해서 DBMS의 트랜잭션이 가져야하는 특성입니다.  

1. Atomicity 원자성
  - 트랜잭션의 연산은 데이터베이스에 모두 반영되도록 commit되든지 아니면 전혀 반영되지 않도록 복구Rollback되어야합니다.
  - 트랜잭션 내의 모든 명령은 반드시 완벽히 수행되어야 하며, 모두가 완벽히 수행되지 않고 어느 하나라도 오류가 발생하면 트랜잭션 전부가 취소 되어야 합니다. 
1. Consistency 일관성 
  - 트랜잭션이 그 실행을 성공적으로 완료하면 언제나 일관성 있는 데이터베이스 상태로 변환됩니다.
  -즉, 시스템이 가지고 있는 고정 요소(제약조건 등)은 트랜잭션 수행 전과 후에 동일해야 합니다. 
1. Isolation 독립성
  - 둘 이상의 트랜잭션이 동시에 병행 실행되는 경우 어느 하나의 트랜잭션 실행 중에 다른 트랜잭션의 연산이 끼어들 수 없습니다.
  - 수행중인 트랜잭션은 완전히 완료될 때까지 다른 트랜잭션과 수행 결과를 참조할 수 없습니다.
1. Durability 지속성
  - 성공적으로 완료된 트랜잭션의 결과는 시스템이 고장나도 영구적으로 반영되어야 합니다.  

# CRUD 매트릭스

CRUD 매트릭스는 2차원 형태의 표로서, 행에는 프로세스, 열에는 테이블, 행과 열이 만나는 위치에는 프로세스가 테이블에 발생시키는 변화가 표시됩니다.  

각 셀에 여러 가지 CRUD 연산이 수행된다면 **C > D > U > R** 순서대로 표기하고 소스코드에 반영하는 것이 바람직합니다.  


| | 회원 | 상품 | 주문 |
|:--|:--|:--|:--|
| 주문요청 | R | R | C | C |

## Reference

- 개인 정처기 공부 자료

**Success Notice:**  
수고하셨습니다. :+1:
{: .notice--success}