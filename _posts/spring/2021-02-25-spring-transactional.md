---
title: "[Spring] FetchType LAZY와 @Transactional"
excerpt: "영속성. LazyInitializationException 원인과 해결"
date: 2021-02-25
last_modified_at:
categories:
  - Spring
tags:
  - Spring
  - org.hibernate.LazyInitializationException
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

# Persistence 영속성

`Persistence영속성`는 데이터를 생성한 프로그램이 종료되더라도 사라지지 않는 데이터의 특성을 말합니다.  

persistence는, 트랜잭션이 무결성을 가지기 위해서 지켜야하는, ACID에서 Duration과 개념상으로 조금 헷갈릴 수 있습니다. ACID의 D는 Duraion으로 성공된 트렌젝션의 결과는 시스템이 고장나도 영구적으로 보존된다는 특징입니다. 굳이 구분하자면 Persistence는 데이터에 대해서, Duration은 transaction에 대한 특성입니다.  

다시 돌아와서 영속성을 가지지 않는 데이터는 프로그램이 종료되면 사라집니다. 메모리 상에 존재하는 데이터에 영속성을 부여하기 위해서는 데이터베이스에 저장을 해야합니다.  

# 영속성과 @Transactional

org.hibernate.LazyInitializationException 오류는 데이터가 영속성을 잃었을 경우 생깁니다. 영속성을 잃었다는 것은 데이터를 생성한 프로그램이 종료되면 해당 데이터는 메모리에만 남아있고, DB에 적재 또는 갱신이 불가능하다는 뜻입니다.  

코드로 이해해보겠습니다. 

```java
public class User {
    // ...
    @OneToMany(fetch = FetchType.LAZY, mappedBy = "user")
    private List<UserItem> userItemList;
}

public class UserRepositoryTest extends ApplicationTest {

    @Autowired
    UserRepository userRepository;

    @Test
    public void read(){
        Optional<User> user = userRepository.findById(3L);
        user.ifPresent(selectedUser -> {
            selectedUser.getUserItemList().stream().forEach(userItem -> {
                System.out.println(userItem.getItem());
            });

            System.out.println("user :"+selectedUser);
        });
    }
```  

위 코드의 경우 userRepository.findByid()를 호출한 이후 return 되는 user 객체는 메모리에만 존재합니다. 따라서 user로부터 getUserItemList()를 호출하는 순간 user는 영속성을 잃었기 때문에 userItemList를 가져오거나, userItem으로부터 item 정보를 조회할 수 없습니다. 이미 DB와의 영속성이 끊어졌으니까요.  

## 해결 방법 1 (지양해야하는 방법)

FetchType.EAGER을 사용하면 됩니다. 이 경우 User -> userItemList -> item 정보를 모두 Join해서 한 번에 가져올 수 있습니다.  

```java
public class User {
    // ...
    @OneToMany(fetch = FetchType.EAGER을, mappedBy = "user")
    private List<UserItem> userItemList;
}
```

하지만 조회해온 데이터를 사용하지 않을 수 있습니다. 볼륨이 큰 데이터일수록 성능이 많이 저하됩니다.  

## 해결 방법 2 (좋은 해결 방법)

Controller -> Service -> Repository의 흐름에서 두 가지 부분에 @Transactional을 추가할 수 있습니다.

1. Service 자체에 @Transactional 추가
1. Repository의 method에 @Transactional 추가

둘 중에 상황에 맞는 방법을 사용하면 됩니다.  

# Reference

- [Transactional](https://jdm.kr/blog/141)