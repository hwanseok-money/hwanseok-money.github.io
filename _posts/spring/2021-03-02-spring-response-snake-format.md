---
title: "[Spring] API Response JSON Format SNAKE로 변경하는 방법"
excerpt: "@JsonProperty을 사용한 방법과 설정을 사용한 방법"
date: 2021-03-02
last_modified_at:
categories:
  - Spring
tags:
  - Spring
  - json
  - format
  - snake
  - property-naming-strategy
  - SNAKE_CASE
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

# API Response JSON Format SNAKE로 변경하는 방법

## 방법 1

각각의 attribute에 @JsonProperty를 설정한다.  

```java
@Data
@NoArgsConstructor
@AllArgsConstructor
@Builder
public class Header<T> {
    // api 통신 시간
    @JsonProperty("transaction_time")
    private LocalDateTime transactionTime;
    // api 응답 코드
    private String resultCode;
    // api 부가 설명
    private String description;

    private T data;
}
```

## 방법 2

/resources/application.yaml에 아래의 설정을 추가한다.  

```yaml
spring:
  jackson:
    property-naming-strategy: SNAKE_CASE
```

# Reference

- 