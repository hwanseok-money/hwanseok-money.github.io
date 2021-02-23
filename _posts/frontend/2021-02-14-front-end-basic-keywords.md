---
title: "[Frontend] 프론트앤드 기본 키워드 정리"
excerpt: ""
date: 2021-02-14
last_modified_at: 
categories:
  - Frontend
tags:
  - Frontend 
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

**Info Notice:**  
안녕하세요. **HwanSeok**입니다.  
본 포스팅은 Frontend의 기초 개념을 다지는 포스팅입니다.  
{: .notice--info}

- 디자인 패턴 : 공통적으로 발생하는 문제에 대해 재사용 가능한 해결책

- 싱글톤 패턴 :
  - 어떤 클래스의 인스턴스를 여러 개 만들지 않고, 하나만 만들어서 사용하는 방법
  - 인스턴스 생성에 제약을 걸어두고, 유일한 단일 객체를 가리키는 `정적 참조변수`가 필요합니다.

- MVC 패턴 : Model + View + Controller
  - 사용자는 view를 통해 정보를 접하고, controller에게 요청을 보냅니다. controller는 model을 통해 데이터를 가져온 뒤 요청을 수행하고 View에 수행 결과를 보여줍니다.  
  - MVC 각각이 자신의 역할만 수행하기 때문에 효율적입니다. 바꿔 말하면 각각의 역할을 어떻게 나눌 것인지가 중요합니다.  

- 브라우저의 랜더링 과정
  1. 브라우저가 읽어들인 문서를 파싱해서 최종적으로 어떤 내용을 랜더링할지 결정
    - DOM(Document Object Model)이 생성됨 : HTML 요소들의 구조화된 표현
    - CSSOM(Cascading Style Sheets Object Model)이 생성됨 : CSS의 구조화된 표현
  1. DOM과 CSSOM에 의해 `렌더 트리`가 생성됨
  1. 브라우저가 해당 렌더링을 수행

- DOM
  - DOM != HTML
    1. HTML이 유요하지 않은 경우 유효한 형태로 변형됩니다.
    1. Javascript에 의해서 변경되는 것은 DOM입니다. 읽어온 HTML 문서가 아닙니다.
      - document.createElemment("p")에서 변경되는 것은 DOM입니다.
  - DOM != 브라우저에서 보이는 것
    1. html p tag가 style="display:none;"을 가지는 경우에도 DOM에는 포함됩니다.
    1. 위의 경우 p tag는 `렌더 트리`에는 포함되지 않습니다. 
  - DOM != 개발자 도구의 Elements 탭
    1. 개발자 도우의 Elements 탭 = DOM + CSSOM + `렌터 트리`의 일부

- 가상 DOM
  - 변경 사항이 있을 때마다 DOM을 다시 그리면 `렌더 트리`가 매번 새롭게 생성된다
  - 변경 사항은 가상 DOM에 저장되고, 가상 DOM과 DOM 사이의 차이점에 대해서 1번만 `렌더 트리`가 새롭게 생성된다. 
  - React, Vue, Angular 모두 가상 DOM을 사용한다. 

- ECMAScript6, ES6
  - hoisting : 아직 선언되지 않은 변수,함수의 선언부만 끌어 올려서 사용하는 방식
    - var: hoisting 됨, 전역 범위
    - let, const : hoisting 되지 않음. 블럭 범위, 재선언 불가
    - const : 초기값 필수, 값 변경 불가능
  - Class, constructor, extends를 통한 상속
  - Arrow Function : 자신의 this가 bind되지 않고 함수 스코프에서의 this가 적용됩니다.
    ```javascript
        function NumberEx() {
      this.num = 0

      setInterval(() => {
        this.num++ // this is from NumberEx
      }, 1000)
    }
    ```
  - Export, Import를 이용해 function과 variable을 다른 곳에서 사용할 수 있습니다. 
  - promise : 비동기 작업을 위해 콜백 함수를 사용했지만 복잡도가 증가해서 추가된 기능
    - resolve. reject, then, catch의 keyword를 사용
    - promise.all, promise.race
- ECMAScript8, ES8
  - async, await 


- javascript의 GC
  - mark-and-sweep 알고리즘
    1. GC가 `roots`의 목록을 생성. `roots`는 코드에서 계속 참조되는 전역변수들(window 포함)
    1. 모든 roots들을 자식 객체까지 재귀적으로 검사를 진행(활성 상태로 mark)
    1. 활성 상태가 아닌 메모리들을 OS로 반환
    * 예상치 못한 참조Unwanted References가 발생하면 GC되지 못할 수 있다.
  - 메모리 누수의 일반적인 형태
    1. var/let/const가 선언되지 않은 변수는 global 객체 내부에 생성되는 변수가 됩니다.
      - 브라우저에서는 window global 변수 내부에 생성되어서 `roots`에 포함되고 GC되지 않습니다.
      - static method의 내부에서 this.variable ='test'라고 생성하면 this는 window 객체가 되어 같은 현상이 발생합니다.

# Reference

- [DOM, 브라우저의 랜더링 과정](https://wit.nts-corp.com/2019/02/14/5522)
- [자바스크립트에서-메모리-누수의-4가지-형태](https://itstory.tk/entry/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EC%97%90%EC%84%9C-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%88%84%EC%88%98%EC%9D%98-4%EA%B0%80%EC%A7%80-%ED%98%95%ED%83%9C)
**Success Notice:**  
수고하셨습니다. :+1:
{: .notice--success}