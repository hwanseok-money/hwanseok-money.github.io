---
title: "[인턴쉽] 콜라비팀 개발팀 풀스텍 인턴"
excerpt: "2020.09.06 ~ 2020.12.18"
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

# 요약
- 2020.09.06 ~ 2020.12.18
- 개발팀, 풀스텍 인턴
- 콜라비 서비스 백오피스 고도화
- java, spring-boot, mysql, mybatis, git, Mac OS
- [인턴 수료 증명서](/assets/images/about/certification_internship_collabee.pdf)

# 직무  

콜라비 서비스의 백오피스 고도화를 위한 전반적인 업무를 진행했습니다. 요구사항 수집, batabase 설계, backend api 설계 및 개발 그리고 frontend 화면 설계 및 개발까지 모두 진행했습니다.  

# 배운점

## 다중 접속을 고려한 안전설계

1. 진행기간	: 2020-09-06 ~ 2020-12-18(인턴쉽, 콜라비팀)
2. 문제상황 : 여러 사용자의 DB 관련 요청을 안전하게 수행하는 구조에 대해 고민해본 경험이 있습니다. 저는 사내 백오피스에서 '프리셋 데이터'의 CRUD 기능을 추가하기 위해 Database 설계, Backend API 개발 그리고 Frontend 화면 설계를 진행했었습니다. 그런데 여러 사용자의 요청이 동시에 이루어지는 경우, 같은 데이터가 중복되서 저장되는 문제와 저장된 데이터가 사라지는 문제가 발생했습니다.
3. 문제원인 도출 : 원인은 동시 접속한 사용자에 대한 대비가 되어있지 않았던 점이었습니다. 
4. 해결방안 탐색 : 여러 개의 Chrome Tab을 띄워두고 추가적인 테스트를 진행했습니다. 각각의 Chrome Tab들은 고유한 PID를 가지고 있어, 다수의 사용자가 동시에 접속하는 환경을 테스트할 수 있다고 생각했기 때문입니다. 
5. 해결방안 : 첫 째, 중복이 발생할 수 있는 Database Table Column에 Unique 옵션을 추가하였습니다. 둘 째, Backend API에서는 Transaction이 실패한 원인에 따라서 try catch를 적용하여 오류의 원인을 Frontend에 제공했습니다. 셋 째, Frontend에서는 실패 원인을 알려주는 Toast를 띄우고, 필요한 경우 사용자가 Form에 입력했던 데이터를 수정할 수 있도록 유도했습니다. 
6. 결과 : 여러 사용자가 동시에 프리셋 데이터의 CRUD 기능을 문제없이 사용할 수 있었습니다. 
7. Skill 또는 지식 : React, Typescript, Spring Boot, Mybatis, MySQL

## 누구나 이해할 수 있는 화면설계  

1. 진행기간	: 2020-09-06 ~ 2020-12-18(인턴쉽, 콜라비팀)
2. 문제상황 : 수많은 버튼을 포함하는 페이지의 직관적인 화면 설계에 대해서 고민해본 경험이 있습니다. 제가 개발했던 사내 백오피스의 '프리셋 페이지'는 데이터의 CRUD 기능이 모두 포함된 페이지였습니다. 수 많은 버튼들이 각각의 CRUD 기능을 수행하고 있었고, 3개의 select box를 사용하여 데이터를 조회하는 등 화면구성이 복잡했습니다.     
3. 문제원인 도출 : 적지 않은 사용자들이 해당 페이지의 사용 방법을 저에게 물어보았습니다. 많은 기능과 복잡한 데이터가 사용되는 페이지였지만 효율적인 화면 설계에 대한 고민이 부족했습니다.    
4. 해결방안 탐색 : 사내 백오피스를 사용할 사용자들이 모두 MacOS를 사용해서 업무를 진행하기 때문에, 예상 사용자가 공통적으로 이해하고 있는 화면구성을 찾아보았습니다. 
5. 해결방안 : MacOS Finder의 Folder Tree 구조로 화면 구성을 변경했습니다.
6. 결과 : 개선 후에는 해당 페이지가 제공하는 다양한 기능을 어려움 없이 이용할 수 있었다는 피드백을 받았습니다.    
7. Skill 또는 지식 : React, Typescript, Spring Boot, Mybatis, MySQL

## 1+N Problem  

1. 진행기간	: 2020-09-06 ~ 2020-12-18(인턴쉽, 콜라비팀)
2. 문제상황 : Database의 1+N Problem을 해결했던 경험이 있습니다. Company Table에는 회사 정보가 저장되어 있었고, 각각의 company에 특정 Column을 추가해야하는 요구사항이 발생했습니다. 하지만 일부 company 정보에만 Column이 추가되기 때문에 기존의 Company Table을 수정하면 NULL 값이 많이 생기는 문제가 있었습니다. 그래서 저는 별도의 Company_info Table을 만들어서 필요한 정보를 저장했습니다. 그런데 Company Table과 Company_Info Table에 저장된 데이터를 종합해서 excel 파일로 export할 수 있는 기능을 개발했을 때, 응답시간이 비정상적으로 느린 문제를 발견했습니다.
3. 문제원인 도출 : 문제의 원인은 SQL query log를 통해 파악할 수 있었습니다. Company 정보를 조회한 뒤 Object 타입으로 List에 저장하고, List를 순회하면서 각각의 company.id에 대응되는 company_info를 조회하다보니 1+N Problem이 발생했던 것입니다.
4. 해결방안 탐색 : Company Table의 전체 데이터를 조회하지 않고, pagination을 통해 제한된 수의 Row만을 조회하는 특성을 파악하였습니다.  
5. 해결방안 : 첫 째, company 정보를 조회한 뒤 List에 Object type으로 저장했습니다. 둘 째, Object List로부터 object.id들을 "1,3,5" 형태의 String으로 추출했습니다. 셋 째, Left Outer Join과 Where In을 사용하였습니다.  
6. 결과 : 1+N 번의 쿼리를 1+1번의 쿼리로 축소하여 excel download API의 수행속도를 5초에서 2초로 크게 줄일 수 있었습니다. 
7. Skill 또는 지식 : Spring Boot, Mybatis, MySQL

## 불필요하게 반복되는 쿼리  

1. 진행기간	: 2020-09-06 ~ 2020-12-18(인턴쉽, 콜라비팀)
2. 문제상황 : on duplicate key update 구문을 사용해서 SQL query를 간소화한 경험이 있습니다. 다양한 API를 개발할 때 이미 저장된 데이터라면 Update를 수행하고, 아니라면 Insert를 수행하는 경우가 많았습니다.
3. 문제원인 도출 : 데이터를 저장할 때 비슷한 로직이 반복된다는 점을 파악했습니다.
4. 해결방안 탐색 : 사내 선배님께 해당 문제를 말씀드렸고 on duplicate key update를 찾아보라는 말씀을 해주셨습니다.
5. 해결방안 : on duplicate key update를 사용하여, 반복되는 로직을 간결하게 수행할 수 있었습니다.  
6. 결과 :  불필요한 소스코드와 SQL 쿼리의 양을 줄여 개발 복잡도를 낮출 수 있었습니다. 
7. Skill 또는 지식 : Spring Boot, Mybatis, MySQL

**Success Notice:**  
감사합니다! :+1:
{: .notice--success}