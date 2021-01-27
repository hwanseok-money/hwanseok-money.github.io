---
title: "[Backend] PostgreSQL과 MariaDB"
excerpt: "Django의 CRUD를 중심으로"
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

# MySQL와 MariaDB

MySQL을 오라클이 인수한 이후 엔터프라이즈 버전으로 유료 배급하고 있습니다. 소스코드도 비공개로 전환되었기 때문에, 오픈소스 진영에서는 MariaDB라는 이름으로 개발되고 있습니다.  

# 용어 정리

- OLTP (OnLine Transaction Processing) : `실시간 업무처리에 최적화`된 프로세스를 말합니다. 가장 우선시 하는것은 업무의 효율적인 처리입니다.
- OLAP (OnLine Analytical Processing) : 다차원으로 이루어진 데이터로 부터 통계적인 요약정보를 제공하고, 의사 결정에 도움이 되는 `데이터 분석 업무에 최적화`된 것을 일컫습니다.
- DW (Data Warehouse) : 오랜기간을 통해 `축척된 데이터를 하나의 통합 데이터베이스`로 구축해 놓은 것을 의미합니다.
- InnoDB : MyISAM과 더불어서 MySQL의 storage Engine입니다.  
- Write-Ahead Logging : DB에서 ACID의 특성 가운데 원자성과 내구성을 제공하는 기술의 한 계열이다. WAL을 사용하는 시스템에서 모든 수정은 적용을 하기전에 로그에 기록된다. 트랜잭션이 종료되었을 때 먼저 기록한 로그를 기준으로 Atomicity와 Consistency를 유지하기 위해 Roll-Back을 수행할지 말지를 결정한다. 
- 샤딩 :같은 테이블 스키마를 가진 데이터를 다수의 데이터베이스에 분산하여 저장하는 방법을 의미합니다.  


# PostgreSQL과 MariaDB

PostgreSQL을 전자, MariaDB를 후자라고 칭하겠습니다. 전자는 `멀티 프로세스`방식이고, 후자는 `멀티 쓰레드` 방식을 사용하고 있습니다. 여기서 오는 가장 큰 차이점은 CPU 멀티코어의 사용 여부입니다. 멀티 프로세스를 사용하는 전자의 경우, 복잡한 쿼리나 Join의 처리 방식에서 조금 더 뛰어난 성능을 보여줍니다. 후자의 경우 join이 중첩루프 방식으로 실행되어 코어를 1개밖에 사용하지 않습니다. 따라서 복잡한 쿼리나 Join에서는 성능저하가 발생할 수 있습니다.  

| | PostgreSQL | MariaDB  |
|:----------|:----------|:---------- |
| 방식 | Multi Processes | Multi Threads |
| 성능| 복잡한 쿼리를 실행해야 하는 환경에서 더 뛰어나다.<br> 하드웨어의 읽기/쓰기 속도가 받쳐줘야 하며, 광범위한 데이터 분석, DW, 데이터 분석 응용 부분에서 뛰어난 성능을 보여준다.<br> Disk I/O가 많은 편으로 HDD 환경보다는 SSD 환경을 추천한다.| 단순한 데이터 트랜잭션에 뛰어남.<br> OLTP/OLAP 시스템에서 읽기 속도만 필요한 경우 좋은 성능을 보여준다.<br> InnoDB는 OLTP/OLAP 환경에서 READ/WRITE 모두 뛰어난 성능을 보여준다.<br> 복잡한 쿼리를 실행해야 하는 환경에서는 성능 저하 발생. |
| SQL Compliance | SQL: 2011의 대부분의 기능을 지원한다. 완전한 Core 적합성을 위해 필요한 179 개의 필수 기능 중 PostgreSQL은 최소 160 개를 준수한다. 또한 지원되는 선택 사양 기능 목록이 많이 있다. | MariaDB는 일부만 준수하고 있다. |
| ACID | PostgreSQL은 처음부터 ACID 를 지향했으며 모든 요구사항을 만족한다.| MariaDB는 InnoDB를 사용했을 때만 만족한다. |
| High Availability | Wal log를 이용한 replication 구축.<br> Master – Slave의 구조를 가지고 있으나, 단순 조회 업무라면 slave에서도 조회가 가능하다.<br> 기본적으로 Slave를 Master로 승격시키면 기존 Master가 Slave 역할을 하는 것이 아니기 때문에 M-S-S의 3노드 구성을 권장한다. | 갈레라 클러스터를 이용한 Master – Master 구성 방식을 사용한다. 3 노드를 권장한다. |
| Materialized Views | 지원 | 지원하지 않음 |
| Programming Languages | DB 단에서 C/C++, Java, JavaScript, .Net, R, Perl, Python, Ruby, Tcl 등 많은 프로그래밍 언어를 지원. | 지원하지 않음 |  

일반적으로 PostgreSQL는 좀 더 큰 규모의 비지니스에서 복잡한 쿼리를 사용하는 OLTP 환경 또는 많은 저장 데이터를 분석하고 응용할수 있는 OLAP 환경에서 많이 선택을 합니다. 병렬쿼리 기능이 구현되어 있어 멀티 쓰레드에서 쿼리를 처리할 수 있습니다. 빠르게 버전업이 되는 오픈소스이기 때문에 한국어로 된 자료가 많지 않습니다. 오라클이나 MySQL 만큼의 레퍼런스 문서가 없고, 실제 운영에 있어 가이드 부분에서 어려운 부분이 있습니다. 또, 클라우드 환경에서 Scale-out하기 어렵습니다.  

MariaDB는 단순한 트랜잭션 처리를 위한 OLTP/OLAP 환경에 유용하며, 윕 기반의 서비스 용도, 서비스가 중지되지 않도록 갈레라 클러스터를 이용한 Master-Master 구조가 필요한 환경에서 이점이 있으며, 플러그인 방식의 엔진 사용으로 사용자가 원하는 타입의 엔진을 사용할 수 있습니다. 기존에 MySQL 엔터프라이즈에서 플러그인으로 제공한 쓰레드풀 기능이 내장됐으며, 스토리지 엔진을 활용한 샤딩 기술을 제공합니다. 즉, MySQL의 오픈소스 버전을 넘어 모든 버전을 대체할 수 있는 특징들을 갖추고 있습니다. 물론 MySQL 8버전이 출시된 시점에 MariaDB도 10.4 버전부터는 MySQL과 완전 독립을 선언했습니다. 따라서 MySQL 8 이상의 버전과의 호환성은 앞으로 장담 할 수 없습니다. 

## Reference

- <https://rastalion.me/postgresql%EA%B3%BC-mariadb%EC%9D%98-%EC%82%AC%EC%9D%B4%EC%97%90%EC%84%9C%EC%9D%98-%EC%84%A0%ED%83%9D/>
- <https://nesoy.github.io/articles/2018-05/Database-Shard>
**Success Notice:**  
수고하셨습니다. :+1:
{: .notice--success}