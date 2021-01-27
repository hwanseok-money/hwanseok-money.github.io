---
title: "[Backend] MyISAM과 InnoDB"
excerpt: "MySQL의 storage engine"
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

# MyISAM

ISAM은 Indexed Sequentiall Access Method의 단점을 보완하기 위해 나온 업그레이드 버전입니다. 이 엔진은 non-transactional-safe 테이블을 관리합니다. 뒤에서 설명할 InnoDB에 비해서 단순한 기본 모델이라고 보면 됩니다. 따라서 전체적으로 속도가 InnoDB보다 빠릅니다. 특히 Select 작업이 빠르다고 합니다. 하지만 결정적으로 데이터 무결성이 보장되지 않아서, 무결성 체크는 개발자나 DBA가 해야합니다. `Table-Level Lock`을 사용해서 Insert과 Update의 속도가 느립니다. 

# InnoDB

MyISAM과 달리 무결성을 보장하기 위해서 ACID 특성을 가지고 있습니다. 때문에 MariaDB의 경우에도 storage engine으로 InnoDB를 사용하는 경우에만 ACID를 보장할 수 있습니다. `Row-Level Lock`을 사용해서 Insert, Update, Delete에 대한 속도가 빠르다는 장점이 있습니다. 하지만 `데이터 모델 디자인`에 많은 시간이 필요하다는 점과 시스템 자원을 많이 사용한다는 단점이 있습니다. 그리고 `Full Text Indexing`이 불가능합니다.  

# Full Text Index

A full-text index is a special type of index that provides index access for full-text queries against character or binary column data.  A full-text index breaks the column into tokens and these tokens make up the index data.

## Why use a Full Text Index?

While regular clustered and non-clustered indexes give us the ability to index most column datatypes they unfortunately are not supported for any of the large object datatypes(LOB). Full-text indexes can however can be created on LOB datatype columns like **TEXT**, VARCHAR(MAX), IMAGE, VARBINARY(MAX) (it can also index CHAR and VARCHAR column types).  **Without this functionality any query that referenced a column defined with a LOB datatype would require a full scan.**

# 동시에 사용 가능한가?

동시에 사용 가능하지만 Storage Engine을 각각 백업해야하고, Lock의 기준이 Table과 Row로 다르기 때문에 이에 따른 복잡도가 증가한다는 단점이 있습니다.  

## Reference

- https://ojava.tistory.com/25

**Success Notice:**  
수고하셨습니다. :+1:
{: .notice--success}