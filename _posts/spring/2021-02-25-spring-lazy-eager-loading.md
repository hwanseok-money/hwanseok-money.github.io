---
title: "[Spring] JPA 지연 로딩과 즉시 로딩"
excerpt: "FetchType LAZY, EAGER"
date: 2021-02-25
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

# JPA

Java Persistence API  

JPA에서 테이블 간 연관 관계는 객체의 참조를 통해 이루어집니다. 서비스가 커질 수록 연관 관계는 복잡해집니다. 그리고 각각의 객체가 가진 정보도 많아집니다.  

객체 정보를 조회할 때 참조하는 객체들의 정보까지 모두 한 번에 가져오면 부담이 커집니다. 따라서 JPA는 참조하는 객체들의 데이터를 가져오는 시점을 정할 수 있는데, 이것이 FetchType입니다.  

- FetchType.EAGER : 데이터를 미리 읽어옵니다.
- FetchType.LAZY : 실제 요청하는 순간 가져옵니다.
  - getter로 접근할 때 참조 객체들의 데이터를 가져옵니다.    
  - N+1 문제가 발생할 수 있습니다.

## N+1 문제가 발생하는 경우

Academy : Subject = 1 : N라고 해보겠습니다.  

아래와 같은 코드에서 'academyRepository.findAll()'에서 전체를 조회하는 쿼리 1번을 수행합니다. 그리고 stream에서 각각의 subject를 조회하는 쿼리를 N번 수행합니다.  

```java
public class Academy {
  // ...
  @OneToMany(cascade = CascadeType.ALL)
  @JoinColumn(name="academy_id")
  private List<Subject> subjects = new ArrayList<>();
}

public class Subject {
  // ...
  @ManyToOne(fetch = FetchType.LAZY)
  @JoinColumn(name = "academy_id", foreignKey = @ForeignKey(name = "FK_SUBJECT_ACADEMY"))
  private Academy academy;
}

public class AcademyService {
  @Autowired
  private AcademyRepository academyRepository;

  @Transactional(readOnly = true)
  public List<String> findAllSubjectNames(){
      return extractSubjectNames(academyRepository.findAll()); // 쿼리 1 번 수행
  }

  /**
    * Lazy Load를 수행하기 위해 메소드를 별도로 생성
    */
  private List<String> extractSubjectNames(List<Academy> academies){
      log.info(">>>>>>>>[모든 과목을 추출한다]<<<<<<<<<");
      log.info("Academy Size : {}", academies.size());

      return academies.stream()
              .map(a -> a.getSubjects().get(0).getName()) // 쿼리 N번 수행
              .collect(Collectors.toList());
  }
}
```

## 해결방법 1. Join Fetch(Inner Join을 사용하는 방법)

repository에서 @Query를 사용하면 fetchType.LAZY여도 연관 객체까지 한 번에 조회를 합니다.  

```java
@Repository
public interface AcademyRepository extends JpaRepository<Academy, Long> {
  /**
  * 1. join fetch를 통한 조회
  */
  @Query("select a from Academy a join fetch a.subjects")
  List<Academy> findAllJoinFetch();
}
```

subject의 하위 entity까지 한 번에 조회하는 경우에는 두 번의 fetch join을 사용하면 됩니다.  

```java
@Repository
public interface AcademyRepository extends JpaRepository<Academy, Long> {
  /**
  * 5. Academy+Subject+Teacher를 join fetch로 조회
  */
  @Query("select a from Academy a join fetch a.subjects s join fetch s.teacher")
  List<Academy> findAllWithTeacher();
}
```  

하지만 이 방법은 쿼리문이 추가됩니다. inner join을 사용합니다.  

## 해결방법 2. @Entity graph (Outer Join을 사용하는 방법)

쿼리를 조금 더 간단하게 하고, @EntityGraph를 사용하면 LAZY가 아닌 EAGER로 조회를 합니다. 이 방법은 Outer Join을 사용합니다.  

```java
@Repository
public interface AcademyRepository extends JpaRepository<Academy, Long> {
  /**
  * 2. @EntityGraph
  */
  @EntityGraph(attributePaths = "subjects")
  @Query("select a from Academy a")
  List<Academy> findAllEntityGraph();
}
```

```java
@Repository
public interface AcademyRepository extends JpaRepository<Academy, Long> {
  /**
  * 6. Academy+Subject+Teacher를 @EntityGraph 로 조회
  */
  @EntityGraph(attributePaths = {"subjects", "subjects.teacher"})
  @Query("select a from Academy a")
  List<Academy> findAllEntityGraphWithTeacher();
}
```

## WIP

inner join과 outer join을 정리한 뒤 포스팅을 계속합니다.  

# Reference

- 초보 웹 개발자를 위한 스프링 5 프로그래밍 입문, 최범균
- [LAZY](https://velog.io/@bread_dd/JPA%EB%8A%94-%EC%99%9C-%EC%A7%80%EC%97%B0-%EB%A1%9C%EB%94%A9%EC%9D%84-%EC%82%AC%EC%9A%A9%ED%95%A0%EA%B9%8C)
- [해결방법 두가지](https://jojoldu.tistory.com/165)