---
title: "[백준]브3~실4/시리즈/피보나치 수"
excerpt: ""
date: 2021-01-02
categories:
  - algorithm
tags:
  - algorithm
  - practice
  - boj
  - "2747"
  - "10870"
  - "2748"
  - "10826"
  - 피보나치 수
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

```
**Info Notice:**  
피보나치 수를 구하는 여러 가지 방법을 알아보겠습니다. 아래 문제 링크의 순서대로 난이도가 높습니다. 
{: .notice--info}

**Warning Notice:**
{: .notice--warning}

**Danger Notice:**
{: .notice--danger}

**Success Notice:**
{: .notice--success}
```

## 문제 링크

[피보나치 수/브3](boj.kr/2747)  
[피보나치 수5/브2](boj.kr/10870)  
[피보나치 수2/실5](boj.kr/2748)  
[피보나치 수4/실4](boj.kr/10826)  
[피보나치 수5/골2](boj.kr/2749)  

## 첫 번째 풀이 : 배열에 저장

### 알고리즘

1. 피보나치 수를 배열에 저장하는 방법을 사용한다.

### 정답 코드

```cpp
#include <iostream>

using namespace std;

int main(void) {
  int n = 0;
  cin >> n;

  int fibo[21];
  fibo[0] = 0;
  fibo[1] = 1;
  for (int i = 2; i <= n; i++) {
    fibo[i] = fibo[i - 1] + fibo[i - 2];
  }
  cout << fibo[n];

  return 0;
}
```

## 두 번째 풀이 : 재귀함수

### 알고리즘

1. 재귀함수를 사용한다.

### 정답 코드

```cpp
#include <iostream>

using namespace std;

int main(void) {
  int n = 0;
  cin >> n;

  int fibo[21];
  fibo[0] = 0;
  fibo[1] = 1;
  for (int i = 2; i <= n; i++) {
    fibo[i] = fibo[i - 1] + fibo[i - 2];
  }
  cout << fibo[n];

  return 0;
}
```

## 세 번째 풀이 : 재귀함수 + 방문 여부

### 알고리즘

1. 재귀함수를 사용한다.
2. 한 번 계산된 피보나치 수는 저장해두고 다시 구하지 않는다.
3. long long을 사용해야 한다. 

### 정답 코드

```cpp
#include <iostream>

#define MAX 10001
using namespace std;

bool visited[MAX];
long long value[MAX];

long long fibo(int n) {
  if (n == 0) return 0;
  else if (n == 1) return 1;
  
  if (visited[n]) return value[n];
  else {
    value[n] = fibo(n - 1) + fibo(n - 2);
    visited[n] = true;
    return value[n];
  }
}

int main(void) {
  int n = 0;
  cin >> n;

  cout << fibo(n);

  return 0;
}
```

## 네 번째 풀이 : string

### 알고리즘

1. long long의 범위를 벗어나기 때문에 string을 사용해야 한다.
2. string 기반 덧셈을 수행하는 방법을 구현한다. 

### 정답 코드

```cpp
#include <iostream>
#include <string>
#include <algorithm>
using namespace std;

string Add(string& s1, string& s2) {
  string result(max(s1.size(), s2.size()), '0');
  bool carry = false;

  for (int i = 0; i < result.size(); i++) {
    int temp = carry;
    carry = false;

    if (i < s1.size()) {
      temp += s1[s1.size() - i - 1] - '0';
    }
    if (i < s2.size()) {
      temp += s2[s2.size() - i - 1] - '0';
    }
    if (temp >= 10) {
      carry = true;
      temp -= 10;
    }
    result[result.size() - i - 1] = temp + '0';
  }
  if (carry) {
    result.insert(result.begin(), '1');
  }
  return result;
}



int main(void) {
  int n = 0;
  cin >> n;
  string a = "0"; // i번째 피보나치 수
  string b = "1"; // i+1번째 피보나치 수
  if (n == 0) cout << a;
  else if (n == 1) cout << b;
  else {
    string result; // i+2번째 피보나치 수
    for (int i = 2; i <= n; i++) {
      result = Add(a, b);
      a = b;
      b = result;
    }
    cout << result;
  }
  return 0;
}
```

## 다섯 번째 풀이 : 행렬의 거듭제곱

### 알고리즘

[여기](https://m.blog.naver.com/jh05013/220999768783)에 큰 수의 피보나치를 구하는 방법이 정리 되어 있습니다. F0은 0이고, F1은 1이니 행렬의 거듭제곱만 구할 수 있으면 됩니다. 

### 정답 코드

이 문제는 지금의 저에게 너무 어려워서 풀지 않겠습니다.

## 여섯 번째 풀이 : 피사노 주기

### 알고리즘

[여기](https://www.acmicpc.net/blog/view/28)에 피사노 주기에 대한 설명이 나와있습니다.

### 정답 코드

이 문제는 지금의 저에게 너무 어려워서 풀지 않겠습니다.

## 결론

**Success Notice:** 
{: .notice--success}
 
