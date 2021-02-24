---
title: "[DesignPattern] 싱글톤 패턴 "
excerpt: "Singleton"
date: 2021-02-23
categories:
  - DesignPattern
  - Java
tags:
  - java
  - singleton

toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
classes: wide
---

# Singleton

instance를 만드는 절차를 추상화하는 패턴이다. Log 객체, ThreadPool 객체, WindowAdmin 객체 등 관리 역할을 수행하는 객체는 단 하나의 insance를 갖는 것이 바람직하다.  

단 하나의 instance를 전역변수로 관리할 수도 있다. 하지만 클래스 정보에 유일한 인스턴스로 접근하는 방법을 자체적으로 관리하는 것이 더 좋다.  

# 여러 구현 방법의 공통점

1. private 생성자만을 정의해 외부 클래스에서 instacne 생성을 차단한다.
1. 싱글톤을 구현하고자 하는 클래스 내부에 멤버 변수로 private static 변수를 생성한다.
1. public static 메서드를 통해 외부에서 singleton instace에 접근할 수 있도록 한다.  

## 방법 1 : Eager Initialization

- 해당 인스턴스를 사용하지 않을 때에도 인스턴스를 생성합니다.
- 따라서 File System, Database Connection과 같은 큰 리소스를 사용하는 경우에는 적합하지 않습니다. 이 경우 getInstance()를 호출하기 전까지 인스턴스를 생성하지 않는 것이 좋습니다.  
- Exception handling을 제공하지 않습니다.  

```java
public class Singleton{
  private satic final Singleton instance = new Singleton();

  pricate Singleton(){}

  public static Singleton getInstance(){
    return instance;
  }
}
```

## 방법 2 : Static Block Initialization

- 해당 인스턴스를 사용하지 않을 때에도 인스턴스를 생성합니다.
- 따라서 File System, Database Connection과 같은 큰 리소스를 사용하는 경우에는 적합하지 않습니다. 이 경우 getInstance()를 호출하기 전까지 인스턴스를 생성하지 않는 것이 좋습니다.  
- 이전 방법에서 Exception handling만을 추가한 코드입니다. 

```java
public class Singleton{
  private static Singleton instance;

  private Singleton(){}

  static{
    try{
      instance = new Singleton();
    }catch(Exception e){
      throw new RuntimeException("Exception occured in creating singleton instance");
    }
  }
  
  public static Singleton getInstance(){
    return instance;
  }
}
```

## 방법 3 : Lazy Initialization

- getInstance()를 호출하기 전까지 인스턴스를 생성하지 않습니다.
- multi-thread 환경에서 동기화 문제가 발생합니다. 여러 개의 thread에서 여러 개의 instance를 생성할 수 있습니다.
- single-thread 환경에서는 사용할 수 있습니다.  
- Exception handling을 제공하지 않습니다. 

```java
public class Singleton{
  private static Singleton instance;

  private Singleton(){}

  public static Singleton getInstance(){
    if(instance == null){
      instance = new Singleton();
    }
    return instance;
  }
}
```

## 방법 4 : Thread Safe Singleton

- 방법 3의 문제에서 synchronized 키워드를 사용해서 multi-thread 환경에서도 사용할 수 있습니다.
- 하지만 singleton instance 호출이 잦은 경우 앱의 성능이 떨어지는 문제가 발생합니다. 

```java
public class Singleton{
  private static Singleton instance;

  private Singleton(){}

  public static synchronized Singleton getInstance(){
    if(instance == null){
      instance = new Singleton();
    }
    return instance;
  }
}
```

## 방법 4-1. double checked locking

좀 더 개선된 방법은 아래와 같습니다.  

```java
public class Singleton{
  private static Singleton instance;

  private Singleton(){}

  public static Singleton getInstance(){
    if(instance == null){
      synchronized(Singleton.class){
        if(instance == null){
          instance = new Singleton();
        }
      }
    }
    return instance;
  }
}
```

## 방법 5 : Bill Pugh Singleton

- getInstance()를 호출할 때 SingletonHelper가 JVM 메모리에 로드되고 인스턴스를 생성합니다.
- synchronized를 사용하지 않아서 성능저하 없이 multi-thread 환경에서 사용할 수 있습니다. 

```java
public class Singleton{
  private Singleton(){}

  // static inner class - inner classes are not loaded until they are referenced.
  /**
     * SingletonHolder is loaded on the first execution of
     * Singleton.getInstance() or the first access to SingletonHolder.INSTANCE,
     * not before.
     */
  private static class SingeltonHelper{
    private static final Singleton INSTANCE = new Singleton();
  }

  public static Singleton getInstance(){
    return SingletonHelper.INSTANCE;
  }
}
```

### 방법 5가 Thread-safe 한 이유

class initialization phase는 JLS(Java Language Specification)에 의해서 serial하게 진행됨이 보장됩니다. 따라서 multi-thread 상황에서도  synchronized 키워드가 필요하지 않습니다.  

### 방법 5를 사용하는 경우

1. initialization 과정의 비용이 높은 경우
1. class-loading phase에 initializeing이 not safe한 경우 사용합니다.  

# Reference

- <https://www.programmersought.com/article/5919280565/>