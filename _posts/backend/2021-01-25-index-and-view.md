---
title: "[Backend] Index와 View"
excerpt: "데이터베이스 기본"
date: 2021-01-27
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

# Index

인덱스는 데이터 레코드를 빠르게 접근하기 위해서 <키, 포인터>쌍으로 구성되는 데이터 구조입니다. 테이블에 데이터가 저장되는데, 특정한 PK값을 가지는 데이터를 찾기 위해서 매번 접근하는 것은 비효율적입니다. 따라서 PK값과 해당하는 데이터 row의 주소를 자료구조로  묶어서 저장하는 것이 인덱스입니다.  

## 특징

- 인덱스는 데이터가 저장된 물리적 구조와 밀접한 관계가 있습니다.
- 인덱스는 레코드가 저장된 물리적 구조에 접근하는 방법을 제공합니다.
- 인덱스를 통해서 파일의 레코드에 대해 엑세스를 빠르게 할 수 있습니다.
- 레코드의  삽입과 삭제가 수시로 일어나는 경우에는 인덱스의 개수를 최소로하는 것이 효율적입니다.
- 인덱스가 없으면 특정한 값을 찾기 위해서 테이블의 모든 데이터를 확인하는 `Table Scan`이 발생합니다.
- 기본키를 위한 인덱스를 기본 인덱스라고 하고, 기본 인덱스가 아닌 인덱스들을 보조 인덱스라고 합니다. 대부분의 관계형 데이터베이스 관리 시스템에서는 모든 기본 키에 대해서 자동적으로 기본 인덱스를 생성합니다.

## 클러스터, 클러스터링

- 클러스터
  - 데이터 저장시 데이터 액세스 효율을 향상시키기 위해서 동일한 성격의 데이터를 동일한 데이터 블록에 저장하는 물리적인 저장방법입니다.
- 클러스터링
  - 두 대 이상의 서버를 하나의 서버처럼 운영하는 기술입니다.
  - 서버 이중화 및 공유 스토리지를 사용하여 서버의 고가용성을 제공합니다.
  - 고가용성을 위해서 사용되는 것이 일반적이고, 성능을 위해서 하나의 작업을 여러 개의 서버에 분산-병렬 처리를 시키기도 합니다.  

## 클러스더드 인덱스, 넌 클러스터드 인덱스

- 클러스터드 인덱스
  - 인덱스의 키의 순서에 따라서 인덱스 데이터가 정려되어서 저장되는 방식입니다.
  - 실제 데이터가 순서대로 저장되어 인덱스를 검색하지 않아도 원하는 데이터를 빠르게 찾을 수 있습니다.
  - 데이터 삽입, 삭제 발생 시 순서를 유지하기 위해 데이터를 재정렬해야 합니다.
  - 한 개의 릴레이션에 하나의 인덱스만 생성할 수 있습니다.
- 넌 클러스터드 인덱스
  - 인덱스의 키 값만 정렬되어 있을 뿐 실제 데이터는 정렬되어 있지 않습니다.
  - 데이터를 검색하기 위해서는 먼저 인덱스를 검색해서 실제 데이터의 위치를 확인해야해서 검색 속도가 떨어집니다.
  - 한 개의 릴레이션에 여러 개의 인덱스를 만들 수 있습니다. 

## B트리, B+트리 인덱스

트리 기반 인덱스는 인덱스를 저장하는 블록들이 트리 구조를 이루고 있는 것을 말합니다. DBMS에서는 트리 구조 기반의 B+ 트리 인덱스를 주로 활용합니다.  

- B 트리 인덱스
  - 일반적으로 사용되는 인덱스 방식으로 루트 노드에서 하위 노드로 키 값의 크기를 비교해 나가면서 단말노드에서 찾고자 하는 데이터를 검색합니다.
  - 키 값과 레코드를 가리키는 포인터들이 트리 노드에 오름차순으로 정렬되어 있습니다.
  - 모든 리프 노드는 같은 레벨에 있습니다. 
- B+ 트리 인덱스
  - B 트리의 변형으로 단말 노드가 아닌 노드로 구성된 `Index Set`와 단말 노드로만 구성된 `Sequence Set`로 구분됩니다. 
  - Index Set에 있는 노드들은 단말 노드에 있는 키 값을 찾아갈 수 있는 경로로만 사용됩니다. 
  - Sequence Set에 있는 단말 노드가 해당 데이터 레코드의 주소를 가리킵니다. 
  - Index Set에 있는 키 값이 Sequnce Set에 다시 나타나므로 단말 노드만을 이용한 순차처리가 가능합니다.  

# Full Text Index

A full-text index is a special type of index that provides index access for full-text queries against character or binary column data.  A full-text index breaks the column into tokens and these tokens make up the index data.

## Why use a Full Text Index?

While regular clustered and non-clustered indexes give us the ability to index most column datatypes they unfortunately are not supported for any of the large object datatypes(LOB). Full-text indexes can however can be created on LOB datatype columns like **TEXT**, VARCHAR(MAX), IMAGE, VARBINARY(MAX) (it can also index CHAR and VARCHAR column types).  **Without this functionality any query that referenced a column defined with a LOB datatype would require a full scan.**

# View

사용자에게 접근이 허용된 자료만을 제한적으로 보여주기 위해 하나 이상의 기본 테이블로부터 유도된, 이름 가진 가상의 테이블입니다. 뷰는 저장장치 내에 물리적으로 존재하지 않지만, 사용자에게는 있는 것처럼 간주됩니다. 조인문의 사용을 최소화하여 편의성을 줍니다. 뷰를 생성하면 뷰 정의가 시스템 내에 저장되었다가 생성된 뷰 이름을 쿼리에서 사용할 경우, 쿼리가 실행될 때 뷰에 정의된 기본 테이블로 대체되어 기본 테이블에서 실행됩니다.  

뷰는 독립적인 인덱스를 가질 수 없다는 특징을 가지고 있습니다.  


## Reference

- https://ojava.tistory.com/25
- https://www.mssqltips.com/sqlservertutorial/9136/sql-server-full-text-indexes/

**Success Notice:**  
수고하셨습니다. :+1:
{: .notice--success}