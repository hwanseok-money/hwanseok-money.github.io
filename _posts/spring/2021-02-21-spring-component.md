---
title: "[Spring] 컴포넌트, Component"
excerpt: "@Component, @ComponentScan"
date: 2021-02-21
last_modified_at:
categories:
  - Spring
tags:
  - Spring
  - Component
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

# 스프링의 Component

Component Scan은 DI와 함께 사용되는 추가 기능이다.

## @ComponentScan

Component Scan은 스프링이 직접 클래스를 검색해서 Bean으로 등록해주는 기능이다. 설정 클래스에서 Bean으로 등록하지 않아도 원하는 클래스를 Bean으로 등록할 수 있게된다.  

@Component Scan을 붙여야, 스프링이 검색해서 Bean으로 등록할 수 있다. class에 @Component를 추가하면 클래스 이름의 첫 문자를 소문자로 바꾼 이름으로 Bean 등록을 해준다. (MemberService Class -> memberService Bean)   

## @Component

Component Scan의 대상으로 지정한다.<br>객체를 생성해서 Bean으로 등록할 Class임을 나타낸다.<br>@Component를 사용하면 설정 클래스에서 직접 Bean으로 등록하지 않아도 된다.  

## 기본 Scan 대상

1. @Component
1. @Controller
1. @Service
1. @Repository
1. @Aspect
1. @Configuration

# Annotation

| 이름 | 설명 |
|:-----|:-----|
| @Configuration | 해당 클래스를 스프링 설정 클래스로 지정 |
| @Bean | 해당 메서드가 생성한 객체를 스프링이 관리하는 빈 객체로 등록<br> |
| @Autowired | 의존 관계에 해당하는 타입의 빈을 찾아서 필드에 할당한다.<br>의존 관계를 설정 클래스에서 명시하지 않아도 된다.<br>메서드에 붙은@Autowired는 해당 메서드의 파라미터 타입에 해당하는 Bean 객체를 찾아서 인자로 주입한다. |
| @Qualifier | @Autowired에 의해 자동 주입되는 객체가 여러 개인 경우 하나를 특정하기 위해서 사용한다.<br>A 타입의 객체를 DI해야하는 경우, A 타입의 객체뿐만 아니라 A타입을 상속한 AA타입의 객체도 DI의 대상이 되어 충돌이 난다.<br>이러한 경우 하나를 특정하기 위해서 사용한다. |
| @Component | Component Scan의 대상으로 지정한다.<br>객체를 생성해서 Bean으로 등록할 Class임을 나타낸다.<br>@Component를 사용하면 설정 클래스에서 직접 Bean으로 등록하지 않아도 된다. |
| @ComponentScan | 설정 클래스에 @Component를 붙혀야, 클래스를 스캔해서 스프링 Bean으로 등록할 수 있다.<br>@ComponentScan(basePackages = {'spring'}은 spring 패키지와 그 하위에 속한 클래스를 스캔 대상으로 설정한다.<br>스캔 대상에 해당하는 클래스 중에서 @Component가 붙은 클래스의 객체를 생성해서 Bean으로 등록한다.|  

# Reference

- 초보 웹 개발자를 위한 스프링 5 프로그래밍 입문, 최범균
