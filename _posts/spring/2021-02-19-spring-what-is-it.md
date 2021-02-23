---
title: "[Spring] 스프링 겉핥기"
excerpt: "스프링은 Bean 객체 컨테이너"
date: 2021-02-19
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

# 자바 버전

- 스프링 5버전 : 자바 8 또는 그 이상
- 스프링 4.3버전 : 자바 6 또는 그 이상

# 스프링

스프링은 스프링 프레임워크 전체를 의미한다.  

## 스프링 프로젝트

스프링 프레임워크는 다양한 스프링 프로젝트를 포함한다. 자주 사용되는 프로젝트는 아래와 같다.

1. 스프링 데이터 : 적은 양의 코드로 데이터 연동을 처리할 수 있도록 도와주는 프레임워크
  - JPA, mongoDB, redis 등 다양한 저장소 기술을 지원한다.
1. 스프링 시큐리티 : 인증/인가와 관련된 프레임워크이다.
  - 웹/객체 접근 제어, 다양한 인증 방식 및 암호화 기능을 제공한다.
1. 스프링 배치 : 배치 처리에 필요한 기본 기능을 제공한다.
  - 로깅, 추적, 작업 통계, 실패 처리 등을 제공한다. 

## 스프링 프레임워크의 특징 

1. DI
1. AOP
1. MVC 웹 프레임워크 제공
1. DB 연동 지원(JDBC, JPA, 선언적 트랜잭션 처리 등)
1. 스케줄링
1. 메시지 연동(JMS)
1. 이메일 발송
1. 테스트 지원

## 스프링은 객체 컨테이너

**Info Notice:**  
어떤 클래스를 사용해서 객체 설정 정보를 가져오든, 설정 정보부터 Bean 이라고 불리는 객체를 생성하고 그 객체를 스프링 컨테이너 내부에 보관한다. ApplicationContext(또는 BeanFactory)는 Bean 객체의 생성,초기화, 보관, 제거 등을 관리하여 (Spring) Container라고도 부른다.
{: .notice--info}

@Bean이 추가된 method는 클래스의 인스턴스를 생성해서 return해주는 역할을 수행한다.
Return된 인스턴스는 main 함수에서 AnnotaionConfigApplicationContext#getBean()을 통해서 사용할 수 있다.
AnnotationConfigApplicationContext는 ApplicationContext 인터페이스를 구현한 클래스로, 
자바 클래스에서 정보를 읽어와서 객체 생성 및 초기화를 수행한다.
한 번쯤 들어봤던 BeanFactory도 interface로, ApplicationContext보다 상위 interface이다.  

```
// 의존 그래프의 일부
BeanFactory(interface)  
<- ApplicationContext(interface) 
<- AnnotationConfigApplicationContext(class)
```  

AnnotationConfigApplicationContext라는 이름에서 알 수 있듯이, Annotation을 통해서 클래스로부터 객체 설정 정보를 가져온다.
XML로 객체 설정 정보를 가져오는 클래스도 존재한다. **어떤 클래스를 사용해서 객체 설정 정보를 가져오든, 설정 정보부터 Bean 이라고 불리는 객체를 생성하고 그 객체를 내부에 보관한다는 점이 중요하다.** ApplicationContext(또는 BeanFactory)는 Bean 객체의 생성,초기화, 보관, 제거 등을 관리하여 (Spring) Container라고도 부른다.

## 기본값은 싱글톤 객체

**Info Notice:**  
@Bean 마다 한 개의 Bean 객체를 생성한다.
{: .notice--info}

별도 설정을 하지 않는 경우 스프링은 한 개의 빈 객체만을 생성한다. 즉, **@Bean마다 한 개의 Bean 객체를 생성한다.** @Bean이 추가된 두 개의 method의 return type이 같으면 각각 다른 인스턴스를 생성해서 보관한다. (각각의 인스턴스는 method의 이름을 통해서 ctx#getBean()할 수 있다.)  

## 스프링 컨테이너의 빈 객체 관리

스프링 컨테이너는 내부적으로 Bean 객체와 Bean 이름을 연결하는 정보를 갖는다. @Bean을 명시한 method의 이름이 Bean 객체의 이름이고, return된 인스턴스가 이름에 대응되는 객체 정보이다.

# Reference

- 초보 웹 개발자를 위한 스프링 5 프로그래밍 입문, 최범균
