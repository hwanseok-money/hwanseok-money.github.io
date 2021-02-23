---
title: "[Spring] 용어 사전 "
excerpt: "JSP, JDBC, MyBatis, ORM, JPA, Hibernate etc"
date: 2021-02-18
last_modified_at:
categories:
  - Spring
tags:
  - Spring
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

# 용어 사전

| 용어 | 설명 |
|:----|:-----|
| Servlet | java 코드 안에 HTML 태그가 삽입되어 있는 .java 파일<br>클라이언트 요청을 처리해서 결과를 전송하는 Servlet 클래스의 구현 규칙을 지킨 자바프로그램 |
| JSP(Java Server Pages) | Servlet을 사용하는 대신 간편한 웹 개발을 위한 기술<br>Java 언어를 기반으로 하는 Server Side 스크립트 언어<br>html안에서 고유의 문법으로 동적인 기능을 제공한다 |
| JDBC | 자바에서 데이터베이스에 접속할 수 있도록 하는 API<br>단점 : 반복되는 코드가 여러 곳에 존재하여 비효율적이다.<br>단점 : java 코드와 sql 코드의 분리가 되지 않아 불편하다. |
| MyBatis | 자바의 RDB 개발을 도와주는 프레임워크<br>장점 : 자바 코드 두 줄로 DB 연동 처리<br>장점 : java 코드와 sql 코드의 분리하여 XML 파일로 관리
| ORM(Object-relational mapping)| 객체 설계와 DB 설계를 중간에서 mapping해주는 기술 |
| JPA(Java Persistence API) | 현재 자바의 ORM 기술의 표준<br>Java APP와 JDBC의 사이에서 동작한다.<br>인터페이스의 모음으로 실제로 동작하지는 않는다. |
| Hibernate | JPA 인터페이스를 구현한 대표적인 오픈소스 |
| Spring | Spring Framework<br>Spring의 3대 요소는 [IoC, DI, AOP]이다. |
| Aspect | AOP에서 여러 객체에 적용되는 공통 기능을 Aspect라고 부른다.<br>트랜잭션이나 보안 등이 Aspect의 좋은 예이다. |
| Advice | 언제 공통 관심 기능을 핵심 로직에 적용할 지를 정의한다.<br>예를 들어 메서드를 호출하기 전(언제)에 트랜잭션 시작(공통 기능) 기능을 적용한다는 것을 정의한다. |
| Joinpoint| Advice를 적용 가능한 지점을 의미한다.<br>메서드 호출, 필드 값 변경 등이 Jointpoint에 해당한다.<br>스프링은 프록시를 이용해서 AOP를 구현하기 때문에 메서드 호출에 대한 Joinpoint만 지원한다. |
| PointCut| Joinpoint의 부분 집합으로서 실제 Advice가 적용되는 Joinpoint를 나타낸다.<br>스프링에서는 정규 표현식이나 AspectJ 문법을 이용해서 Pointcut을 정의할 수 있다. |
| Weaving| Advice를 핵심 로직 코드에 적용하는 것을 weaving이라고 한다.|
| Before Advice |대상 객체의 method 호출 전에 공통 기능을 실행 |
| After Returning Advice |대상 객체의 method가 익셉션 없이 실행된 이후 공통 기능을 실행|
| After Throwing Advice |대상 개게의 method가 익셉션이 발생한 경우 공통 기능을 실행|
| After Advice | 익센션 발생 여부에 상관없이 대상 객체의 메서드 실행 후 공통을 실행(try-catch-finally의 finally와 비슷)|
| Arount Advice| 대상 객체의 메서드 실행 전, 후, 또는 익셉션 발생 시점에 공통 기능을 실행하는데 사용|


# Annotation

| 이름 | 설명 |
|:-----|:-----|
| @Configuration | 해당 클래스를 스프링 설정 클래스로 지정 |
| @Bean | 해당 메서드가 생성한 객체를 스프링이 관리하는 빈 객체로 등록<br> |
| @Autowired | 의존 관계에 해당하는 타입의 빈을 찾아서 필드에 할당한다.<br>의존 관계를 설정 클래스에서 명시하지 않아도 된다.<br>메서드에 붙은@Autowired는 해당 메서드의 파라미터 타입에 해당하는 Bean 객체를 찾아서 인자로 주입한다. |
| @Qualifier | @Autowired에 의해 자동 주입되는 객체가 여러 개인 경우 하나를 특정하기 위해서 사용한다.<br>A 타입의 객체를 DI해야하는 경우, A 타입의 객체뿐만 아니라 A타입을 상속한 AA타입의 객체도 DI의 대상이 되어 충돌이 난다.<br>이러한 경우 하나를 특정하기 위해서 사용한다. |
| @Component | Component Scan의 대상으로 지정한다.<br>객체를 생성해서 Bean으로 등록할 Class임을 나타낸다.<br>@Component를 사용하면 설정 클래스에서 직접 Bean으로 등록하지 않아도 된다. |
| @ComponentScan | 설정 클래스에 @Component를 붙혀야, 클래스를 스캔해서 스프링 Bean으로 등록할 수 있다.<br>@ComponentScan(basePackages = {'spring'}은 spring 패키지와 그 하위에 속한 클래스를 스캔 대상으로 설정한다.<br>스캔 대상에 해당하는 클래스 중에서 @Component가 붙은 클래스의 객체를 생성해서 Bean으로 등록한다.|  
| @Aspect | AOP의 공통 부분을 정의한다. |
| @Order | 다수의 @Aspect가 적용될 때 적용 순서를 지정한다.|

# Reference

- [JSP](https://gmlwjd9405.github.io/2018/11/03/jsp.html)
- [JDBC](https://ko.wikipedia.org/wiki/JDBC)
- [MyBatis](https://sjh836.tistory.com/127)
- [ORM](https://gmlwjd9405.github.io/2019/08/04/what-is-jpa.html)
- [Servlet, JSP](https://m.blog.naver.com/acornedu/221128616501)