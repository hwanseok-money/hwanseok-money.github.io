---
title: "[Spring] Bean LifeCycle"
excerpt: "객체 생성, 의존 설정, 초기화, 소멸"
date: 2021-02-21
last_modified_at:
categories:
  - Spring
tags:
  - Spring
  - Bean
  - lifecycle
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

# 스프링 Bean의 LifeCycle

```java
AnnotationConfigApplicationContext ctx = new AnnotationConfigApplicationContext(AppContext.class); // 1번
Greeter g = ctx.getBean("greeter", Greeter.class); // 2번
String msg = g.greet("스프링");
ctx.close(); // 3번
```

1. 위 코드에서 1번 시점에서 스프링 컨테이너를 초기화한다. 스프링 컨테이너는 설정클래스에서 정보를 읽어와서 알맞은 빈 객체를 생성하고, 각 빈을 DI하는 작업을 수행한다.  
1. 컨테이버 초기화가 완료되면 컨테이너를 2번과 같이 사용할 수 있다. 즉, 컨테이너에 보관된 빈 객체를 구할 수 있다.  
1. 컨테이너 사용이 끝나면 컨테이너를 종료한다.  


컨테이너의 초기화는 (빈 객체의 생성 -> DI -> 초기화)를 의미하고, 컨테이너의 종료는 (빈 객체의 소멸)을 의미한다.  

## 스프링 빈 객체의 라이프사이클 

빈 객체는 4단계의 라이프 사이클을 가진다.

1. 객체 생성
1. 의존 설정
1. 초기화
1. 소멸

### 빈 객체의 생성과 소멸

빈 객체의 생성과 소멸 과정에서는 아래의 인터페이스의 메서드를 호출한다.  

```java
@Configuration
public class AppCtx{
  @Bean
  pubilc Client client(){
    Client client = new Client(); // 1단계 객체 생성
    client.setHost("host"); // 2단계 의존 설정 또는 properties 설정
    return client;
  }
}
```  

```java
public interface InitializingBean{
  void afterPropertiesSet() throws Exception; // 3단계 초기화에서 호출된다.
}

public interface DisposableBean{
  void destroy() throws Exception; // 4단계 소멸 과정에서 호출된다. 
}
```

빈 객체가 InitializingBean을 구현하면 스프링 컨테이너는 3번째 단계인 초기화 과정에서 빈 객체의 afterPropersitesSet()을 호출한다. 초기화와 소멸 과정이 필요한 예로는 DB Connection Pool과 채팅 클라이언트가 있다. 

# Reference

- 초보 웹 개발자를 위한 스프링 5 프로그래밍 입문, 최범균