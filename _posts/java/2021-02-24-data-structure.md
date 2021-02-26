---
title: "[Java] 자료구조"
excerpt: "List, Set, Hash, Tree etc"
date: 2021-02-24
categories:
  - Java
tags:
  - java
  - data structure

toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
classes: wide
---

# Array

- 정적인 길이를 제공하는 배열이다. 
- 논리적인 저장 순서와 물리적 저장 순서가 일치한다.
- Read : O(1) : index로 해당 원소에 접근 가능
- Remove : 최악 O(n) : 빈 공간을 막기 위해서 전체 원소를 shift해야하는 경우
- Add : 최악 O(n) : 빈 공간을 만들기 위해 전체 원소를 shift해야하는 경우

# Collection Framework

- Collection
  - List : Interface. 순서 존재. 중복 허용
    - ArrayList
    - Vector
    - LinkedList
    - Stack
    - Queue
  - Set : Interface. 순서 없음. 중복 비허용.
    - HashSet
    - TreeSet

# List Interface

## ArrayList

- 내부적으로 데이터를 배열에 관리한다.
- 검색 > 추가, 삭제
- 데이터의 추가, 삭제를 위해 임시배열을 생성해서 데이터를 복사하는 방법을 사용한다.
- 대량의 자료를 추가/삭제하는 경우 데이터 복사로 인한 성능 저하가 발생한다.
- 각 데이터는 index를 사용해서 접근할 수 있다.

## Vector

ArrayList의 Thread-safe 버전입니다.

## LinkedList

- 각각의 원소들은 자기 자신 전후의 Node 정보만을 기억하고 있다.
- 추가, 삭제 > 검색
- Read : O(n) : index로 접근이 불가능
- Add : O(N) : 특정 원소가 들어갈 위치를 탐색하기 위한 시간이 소요된다. 
- Remove : O(N) : 지울 특정 원소를 탐색하기 위한 시간이 소요된다. 
- Tree에서 사용되어서 유용한 자료구조로 쓰인다.

# Set Interface

## HashSet

- Set interface의 특징대로 중복된 요소를 저장하지 않는다.
- 이미 저장된 요소와 중복되는 요소를 추가하고자 하면 false를 반환해서 추가 실패를 나타낸다.
- 저장 순서를 유지하지 앟는다.
- 저장 순서를 유지한다면 LinkedHashSet을 사용해야 한다. 
- 초기 Capacity와 LoadFactor를 설정할 수 있다.  
  -  LoadFactor : 저장공간의 몇 %가 채워졌을 때 capacity를 늘릴 것인가? 

## TreeSet

- Set interface의 특징대로 중복된 요소를 저장하지 않는다.
- Binary Search Tree 형태로 데이터를 저장한다.
- TreeSet은 BST의 성능을 향상시킨 Red-Black Tree로 구현되어 있다.
- 정렬된 위치에 저장되기 때문에 저장 순서를 유지하지 않는다.


# Binary Search Tree

- 모든 노드는 최대 2개의 자식 노드를 가질 수 없다.
- 부모노드를 기준으로 왼쪽 자식노드의 값은 부모노드의 값보다 작다.
- 부모노드를 기준으로 오른쪽 자식노드의 값은 부모노드의 값보다 크다.
- 순차적으로 저장되지 않으므로 노드의 추가/삭제에 O(logN)시간이 걸린다.
- 검색과 정렬에 유리하다.
- 중복된 값을 저장하지 못한다.(count 변수를 Node가 가지는 것이 더 효율적이다.)

## LinkedList와 비교

- 데이터 삭제의 경우 트리 일부를 재구성하여, LinkedList보다 데이터 추가,삭제 시간이 더 오래 걸린다.
- 검색과 정렬은 LinkedList보다 뛰어나다.

# HashTable

- 모든 accosicative array와 같이, 아래의 명령을 지원한다.
  1. 키(key)와 값(value)이 주어졌을 때, 연관 배열에 그 두 값(key & value)을 저장하는 명령
  1. 키(key)가 주어졌을 때, 연관되는 값(value)을 얻는 명령
  1. 키(key)와 새로운 값(value)이 주어졌을 때, 원래 키에 연관된 값(value)을 새로운 값(value)으로 교체하는 명령
  1. 키(key)가 주어졌을 때, 그 키(key)에 연관된 값(value)을 제거하는 명령

## 해시 충돌을 피하는 방법

1. 체이닝 해시
  - 해시 충돌이 발생하면 LinkedList로 데이터들을 연결한다.
  - 데이터 쏠림이 발생하는 경우 조회/삽입/삭제에서 O(N)이 발생할 수 있다.
1. 개방 주소법(Open Addressing)
  - 해시 충돌이 발생하면 다른 bucket에 데이터를 삽입한다
  1. 선형 탐색 : 해시 충돌 시 다음 혹은 몇 개의 bucket을 건너뛰고 빈 곳을 찾아서 삽입
  1. 제곱 탐색 : 해시 충돌 시 제곱만큼 건너뛴 bucket에 삽입
  1. 이중 해시 : 해시 충돌 시 다른 해시 함수를 한 번 더 적용한다.

## 체이닝 해시와 개방 주소법 장단점

1. 체이닝 해시
  - LinkedList만 사용하면 된다.
  - LoadFactor가 증가함에 따라 LookUp 성능 저하가 Linear하게 발생한다.
1. 개방 주소법(Open Addressing)
  - 체이닝처럼 포인터가 필요없다.
  - 지정한 메모리 외 추가 저장 공간이 필요없다.
  - 삽입,삭제시 오버헤드가 적다.
  - 저장할 데이터가 적을 때 유리하다
  - LoadFactor가 증가함에 따라 LoopUp 성능 저하가 급격하게 증가한다.
- LoadFactor 0.6~0.7로 유지하는 것이 성능 저하를 막는 방법이다.
- LoadFactor 0.8정도에서는 두 방법의 성능 저하가 비슷하고, 넘어가면 개방주소법이 더 저하가 심하다.

# Reference

- [HashTable](https://velog.io/@cyranocoding/Hash-Hashing-Hash-Table%ED%95%B4%EC%8B%9C-%ED%95%B4%EC%8B%B1-%ED%95%B4%EC%8B%9C%ED%85%8C%EC%9D%B4%EB%B8%94-%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0%EC%9D%98-%EC%9D%B4%ED%95%B4-6ijyonph6o#%ED%95%B4%EC%8B%9C-%ED%85%8C%EC%9D%B4%EB%B8%94hash-table)

 



