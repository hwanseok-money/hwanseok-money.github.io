---
title: "[이론] 플루이드 와샬 Floyd-Warshall "
excerpt: "모든 노드에서 다른 모든 노드까지의 최단 경로 구하기"
date: 2021-01-22
last_modified_at:
categories:
  - Algorithm-Theory
tags:
  - Algorithm-Theory
  - Practice
  - binary-search
  - 이분탐색
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

# 플루이드 와샬

## 알고리즘

각 단계마다 특정한 노드 k를 거쳐 가는 경우를 확인합니다. a에서 b로 가는 최단 거리보다 a에서 k를 거쳐 b로 가는 거리가 더 짧은지 검사합니다.  

$D_{ab} = min(D_{ab}, D_{ak} + D_{kb})$

## 시간복잡도

3중 for문을 사용해서 O(N^3)입니다.  

**Success Notice:**
수고하셨습니다. :+1:
{: .notice--success}