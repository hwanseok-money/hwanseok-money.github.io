---
title: "[Spring] AOP, Aspect Oriented Programming"
excerpt: "@Aspect, @JoinPoint, @Pointcut"
date: 2021-02-23
last_modified_at:
categories:
  - Spring
tags:
  - Spring
  - AOP
  - Aspect Oriented Programming
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

# Proxy란

## 수정사항을 여러 클래스에 모두 작성해야 할까?

Calculator를 구현한 두 가지 Class가 있습니다.  

```java
//Calculator.java
public interface Calculator {
    public long factorial(long num);
}

//ImpeCalculator.java
public class ImpeCalculator implements Calculator {

    @Override
    public long factorial(long num) {
        long result = 1;
        for (long i=1; i<=num; i++){
            result *= i;
        }
        return result;
    }
}

//RecCalculator.java
public class RecCalculator implements Calculator {
    @Override
    public long factorial(long num) {
        if(num == 0) {
            return 1;
        }else{
            return num * factorial(num-1);
        }
    }
}
```

ImpeCalculator와 RecCalculator에 수정사항을 추가하려면 같은 코드를 두 군데에 모두 추가해야합니다. (RecCalculator의 경우 recursive로 작성되어 있어서 try-finally 문을 사용해야할 수도 있습니다.)  

## 해결 방법 : Proxy

아래와 같은 방법을 사용하면 두 가지 이점을 얻을 수 있습니다.

1. 기존 코드를 변경하지 않고, 실행 시간을 출력할 수 있다.
1. 실행시간을 구하는 코드의 중복을 제거할 수 있다.  

```java
///ExeTimeCalculator.java
public class ExeTimeCalculator implements Calculator {

    private Calculator delegate;

    public ExeTimeCalculator(Calculator calculator) {
        this.delegate = calculator;
    }

    @Override
    public long factorial(long num) {
        long start = System.nanoTime();
        long result = delegate.factorial(num);
        long end = System.nanoTime();
        System.out.printf("%s.factorial(%d) 실행 시간 = %d",
                delegate.getClass().getSimpleName(),
                num,
                (end - start));
        return result;
    }
}

// main.java
public class main {
    public static void main(String[] args){
        ImpeCalculator impeCalculator = new ImpeCalculator();
        ExeTimeCalculator exeTimeCalculator = new ExeTimeCalculator(impeCalculator);
        System.out.println(exeTimeCalculator.factorial(20));

        RecCalculator recCalculator = new RecCalculator();
        exeTimeCalculator = new ExeTimeCalculator(recCalculator);
        System.out.println(exeTimeCalculator.factorial(20));

    }
}
```

이러한 장점을 얻을 수 있는 이유는 크게 두 가지 입니다.

1. factorial() 기능 자체를 직접 구현하지 않고, 다른 객체에 factorial()의 실행을 위임했다.
1. 다른 객체가 factorial()의 호출 앞뒤에서 추가적인 기능을 구현했다.  

## Proxy와 Decorator

위와 같은 방식의 코드는 크게 Porxy와 Decorator로 나뉜다. 위에서 작성한 코드는 Proxy보다는 Decorator에 가깝다. 하지만 여전히 Proxy 또는 Decorator를 이해하는 것은 AOP를 이해하는데 중요하다. 

- Proxy : 접근 제어 관점에 초점
- Decorator : 기능 추가와 확장에 초점 

Porxy의 특징 다음과 같다.

1. 핵심 기능을 구현하지 않는다.
1. 대신 여러 객체에 공통으로 적용할 수 있는 기능을 구현한다.

**공통 기능 구현과 핵심 기능 구현을 분리**하는 것이 AOP의 핵심임을 기억하고 넘어가자.  

# Spring AOP

## 핵심 기능에 공통 기능을 삽입하는 AOP

AOP는 여러 객체에 공통으로 적용할 수 있는 기능을 분리해서 재사용성을 높여주는 개발 방법이다. 
AOP를 사용하면 핵심 기능 코드의 수정 없이 공통 기능을 적용할 수 있게 된다. 

핵심 기능에 공통 기능을 삽입하는 방식은 크게 세 가지가 있다.

1. 컴파일 시점에 코드에 공통 기능을 삽입하는 방법
1. 클래스 로딩 시점에 바이트 코드에 공통 기능을 삽입하는 방법
1. 런타임에 프록시 객체를 생성해서 공통 기능을 삽입하는 방법

첫 번째 두 번째 방법은 Srping AOP에서는 제공하지 않고, AspectJ와 같이 AOP 전용 도구를 사용해서 적용할 수 있다. 스프링이 제공하는 AOP 방식은 세 번째 방식이다.  

![spring-aop-proxy](/assets/images/spring/spring-aop-proxy.jpg)  

스프링 AOP는 프록시 객체를 자동으로 만들어준다. 따라서 ExeTimeCalculator 클래스처럼 상위 타입의 interface를 상속받은 proxy 클래스를 직접 구현하지 않아도 된다. 공통 기능을 구현한 클래스만 알맞게 구현하면 된다.  

Advice는 언제 공통 기능을 핵심 로직에 적용할 지를 정의하는 용어이다. 스프링은 proxy를 이용해서 AOP를 구현하기 때문에 메서드 호출에 관련된 적용 시점만 존재한다. Advice를 적용 가능한 지점을 JoinPoint라고 부르기도 한다. 아래는 메서드 호출과 관련된 적용 시점의 예시이다.   

1. 대상 객체의 메서드 호출 전에 공통 기능 실행 (Before Advice)
1. 대상 객체의 메서드가 exception 없이 실행된 이후에 공통 기능 실행 (After Return Advice)
1. 대상 객체의 메서드를 실행하는 도중 exception이 발생한 경우에 공통 기능 실행 (After Throwing Advice)
1. 대상 객채의 메서드에서 exception 발생 여부와 상관없이, 대상 객체의 메서드 실행 후 실행 (After Advice)
1. 대상 객체의 메서드 실행 전, 후 또는 exception 발생 시점에 공통 기능을 실행 (Around Advice)

마지막의 Around Advice를 많이 사용한다. 캐시 기능, 성능 모니터링 기능와 같은 Aspect를 구현할 때 Around Advice를 사용한다. 

| 용어 | 의미 |
|:-----|:-----|
| Advice | 언제 공통 기능을 핵심 로직에 적용할 것인가? |
| JointPoint | Advice를 적용 가능한 지점<br>Spring에서는 Method 호출에 대한 JointPoint만 지원한다. |
| PointCut | JointPoint의 부분 집합<br>실제 Advice가 적용되는 JointPoint<br>정규표현식 등을 사용해서 PointCut을 정의할 수 있다. |

## AOP 예제

```java
// Aspect class
@Aspect
public class ExeTimeAspect {
    @PointCut("execution(public * chap07..*(..))")
    private void publicTarget(){
    }

    @Around("publicTarget()")
    public Object measuer(ProceedingJoinPoint joinPoint) throws Throwable{
        long start = System.nanoTime();
        try {
            Object result = joinPoint.proceed();
            return result;
        } finally {
            long finish = System.nanoTime();
            Signature sig = joinPoint.getSigniture();
            System.out.printf("%s.%s(%s)실행 시간 : %d ns\n",
                    joinPoint.getTarget().getClass().getSimpleName(),
                    sig.getName(),
                    Arrays.toString(joinPoint.getArgs()),
                    (finish-start));
        }
    }
}

//설정 클래스
@Configuration
@EnableAspectJAutoProxy
public class AppCtx {
    @Bean
    public ExeTimeAspect exeTimeAspect(){
        return new ExeTimeAspect();
    }
}

//main
AnnotationConfigApplicationContext ctx = new Anno--(AppCtx.class);
Calculator cal = ctx.getBean("calculator", Calculator.class);
long fiveFactorial = cal.factorial(5);
ctx.close();
```  

- signiture = method name + method parameter

@Aspect를 적용한 클래스는 Advice와 Pointcut을 함께 제공한다. @Pointcut은 공통 기능을 적용할 대상을 설정한다. 위 코드의 @Pointcut은 'chap07 패키지와 그 하위 패키지에 위치한 public 메서드'를 Pointcut으로 설정한다는 뜻이다.(@PointCut을 정의하는 방법은 후술한다.)  

@Around는 Around Advice를 설정한다. @Around의 값이 publicTarget()인데 이는 publicTarget()메서드에 정의한 @PointCut에 공통 기능을 적용한다는 의미이다. 'chap07 패키지와 그 하위 패키지에 위치한 public 메서드'에 @Around가 붙은 measure() 메서드를 적용한다.  

위와 같이 설정을 해두면 아래와 같이 Proxy가 자동으로 생성되고 동작한다.  

> 스프링은 @EnableAspectJAutoProx와 같이 이름이 Enable로 시작하는 다양한 Annotation을 제공한다. @Enable로 시작하는 Annotation은 관련 기능을 적용하는데 필요한 다양한 스프링 설정을 대신 처리한다. 예를 들어 @EnableAspectJAutoProxyCreator은 프록시 생성과 관련된 AnnotationAwareAspectJAutoProxyCreator 객체를 빈으로 등록한다.  

![spring-aop-proxy-example](/assets/images/spring/spring-aop-proxy-example.jpg)  

## Proxy 생성 방식

```java
//main
AnnotationConfigApplicationContext ctx = new Anno--(AppCtx.class);
// Calculator cal = ctx.getBean("calculator", Calculator.class); 수정 전
RecCalculator cal = ctx.getBean("calculator", RecCalculator.class); // 수정 후 Error 발생!
long fiveFactorial = cal.factorial(5);
ctx.close();
```

**스프링은 AOP를 위한 프록시 객체를 생성할 때, 실제 생성할 빈 객체가 interface를 상속하면 inferface를 이용해서 proxy를 생성한다.** 위의 예제에서도 RecCalulator의 Bean을 생성하려고 할 때, Calculator interface를 상속한 proxy 객체를 생성한다.  

즉, Calculator interface를 상속받은 타입의 객체이고 RelCalulator 타입이 아니기 때문에 RecCalculator라고 형변환이 불가능하다는 Erorr가 발생한다.  

**@EnableAspectJAutoProxy(proxyTargetClass = true)를 사용하면 interface가 아닌 java class를 상속받아서 proxy를 생성한다.** calculator interface 대신에 RelCalculator.class를 상속받은 Proxy 타입을 생성한 뒤, RelCalculator로 형변환을 한다.  

```java
//설정 클래스
@Configuration

public class AppCtx {
    @Bean
    public ExeTimeAspect exeTimeAspect(){
        return new ExeTimeAspect();
    }
}
```

## @PointCut을 정의하는 방법(execution 명시자 표현식)

execution(수식어패턴? 리턴타입패턴 클래스이름패턴?메서드이름패턴(파라미터패턴))
- 수식어패턴 : 생략가능하며 public protected 등이온다. 스프링 AOP는 public 메서드에만적용 할 수 있다.
- 메서드이름패턴 set\*: set으로 시작하는 이름을 가진 모든 메서드
- 패키지이름패턴 chap07 : chap07 패키지
- 패키지이름패턴 chap07.. : chap07 패키지와 그 하위 패키지
- 파라미터패턴 (..) : 0개 이상의 파라미터
- 파라미터패턴 (Ingeter, ..) : Ingeter 파라미터 포함해서 1개 이상의 파라미터

| terminology | 수식어패턴? | 리턴타입패턴 | 패키지이름패턴? | 클래스이름패턴? |메서드이름패턴 | 파라미터패턴 |  
|:--------|:--------|:--------|:--------|:--------|:--------|:--------|  
|execution(public void set\*(..))|public| void | 생략 | 생략 | set\* | (..) |  
|execution(\* chap07.\*.\*())|생략| \* | chap07 | \* | \* | () |  
|execution(\* chap07..\*.\*(..))|생략| \* | chap07.. | \* | \* | (..) |  
|execution(Long chap07.Calculator.factorial(..))|생략| Long | chap07 | Calculator | factorial | (..) |  
|execution(\* get\*(\*))|생략| \* | 생략 | 생략 |get\* | (\*) | 
|execution(\* get\*(\*,\*))|생략| \* | 생략 | 생략 | get\* | (\*,\*) |
|execution(\* read\*(Integer, ..)) | 생략 | \* | 생략 | 생략 | read\* | (Integer, ..) | 

## AOP의 활용 : Cache

joinPoint의 args로 구한 key 값이 cache에 존재하면 그 값을 return 한다. 존재하지 않으면 proxy 대상 객체를 실행해서 값을 return 한다.  

```java
@Aspect
public class CacheAspect {
    private Map<Long, Object> cache = new HashMap<>();
    
    @Pointcut("execution(public * chap07..*(long))")
    public void cacheTarget(){
    }
    
    @Around("cacheTarget()")
    public Object execute(ProceedingJoinPoint joinPoint) throws Throwable{
        Long num = (Long) joinPoint.getArgs()[0];
        if(cache.containsKey(num)){
            return cache.get(num);
        }
        Object result = joinPoint.proceed();
        cache.put(num, result);
        return result;
    }
}
```

- CacheAspect Proxy 객체 -> ExeTimeAspect Proxy 객체 -> 실제 대상 객체

위와 같은 순서대로 실제 대상 객체에 두 개의 Proxy가 설정되어 있다고 가정하다. 이 때 main에서의 cal은 CacheAspect 타입의 proxy 객체이다.  

```java
//main
AnnotationConfigApplicationContext ctx = new Anno--(AppCtx.class);
Calculator cal = ctx.getBean("calculator", Calculator.class);
long fiveFactorial = cal.factorial(5);
ctx.close();
``` 

main에서의 cal은 Calculator interface를 상속받은 CacheAspectProxy 타입의 객체가 반환된다. 그리고 cal.factorial(5)을 호출할 때는 아래와 같은 흐름으로 대상객체의 메서드가 호출된다.  

![spring-aop-double-proxy-example](/assets/images/spring/spring-aop-double-proxy-example.jpg)  

## @Enable 설정 세 가지 구현 방식

<https://javacan.tistory.com/entry/spring-at-enable-config>

# Reference

- 초보 웹 개발자를 위한 스프링 5 프로그래밍 입문, 최범균
