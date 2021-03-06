---
title: "[Spring] JPA Auditing"
excerpt: "중복되는 Column 자동으로 채우기"
date: 2021-03-02
last_modified_at:
categories:
  - Spring
tags:
  - Spring
  - JPA 
  - Auditing
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

# Auditing

JPA를 사용할 때 여러 entity에 반복적으로 들어가는 attribute가 있습니다. 데이터의 생성시간/생성주체/수정시간/수정주체 등의 정보는 필수적으로 그리고 공통적으로 관리되는 정보입니다. 하지만 이 값을 매번 직접 입력하는 것은 많이 불편합니다.  

## 적용 방법

controller, service와 같은 레벨의 디렉토리에서 component와 config 디렉토리를 생성합니다.  

```java
//component/LoginUserAuditorAware
@Configuration
public class LoginUserAuditorAware implements AuditorAware<String> {

    @Override
    public Optional<String> getCurrentAuditor() {
        return Optional.of("AdminServer");
    }
}
// config/JpaConfig
@Configuration
@EnableJpaAuditing
public class JpaConfig {
}      
//model/entity/User
@EntityListeners(AuditingEntityListener.class)
public class User {
    @CreatedDate
    private LocalDateTime createdAt;
    @CreatedBy
    private String createdBy;
    @LastModifiedDate
    private LocalDateTime updatedAt;
    @LastModifiedBy
    private String updatedBy;
}
```

# Reference

- [JPA Auditing](https://webcoding-start.tistory.com/53)