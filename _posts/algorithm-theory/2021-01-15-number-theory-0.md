---
title: "[이론][정수론] 소인수 분해 "
excerpt: "N이 10억 이상인 경우 소인수 분해 방법"
date: 2021-01-15
last_modified_at:
categories:
  - Algorithm-Theory
tags:
  - Algorithm-Theory
  - Practice
  - Number Theory
  - 정수론
  - "11653"
  - 소인수분해
  - "2004"
  - 조합 0의 개수
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

## 겁먹지 않습니다!  

N이 10억 이상이어도 동작하는 방법입니다. 먼저 N이 매우 커도(10억 쯤) N의 `약수의 종류`는 많지 않습니다.  

$2 * 3 * 5 * 7 * 11 * 13 * 17 * 19 = 9,699,690$  

또한 `약수의 갯수`도 많지 않습니다. 거듭 제곱꼴로 표현해도 최대 30개 정도입니다.   

$2^{31} = (2^{10})^3 * 2 = 1024^3 * 2 \approx 10^9 \approx 10억$

## 약수 구하기

[문제링크](https://www.acmicpc.net/problem/11653)  

### 알고리즘

N을 약수들의 곱으로 표현하다면 다음과 같습니다.

```
N = a // N이 소수인 경우  
N = a * b  // N이 소수가 아닌 경우  
```  

a < b라는 조건에 따라서 N을 표현한다고 가정하겠습니다.  
이 때 `a<sqrt(N)`라는 조건을 가집니다.  

```
// a < b 인 경우
A = a * a // sqrt(A) = a  
A = a * b // a < sqrt(A) < b   
A = b * b // sqrt(A) = b  
```  

따라서 N의 약수를 구하기 위해서는 다음의 코드처럼 i의 범위를 `i*i<=N`을 만족하는 구간으로 설정해도 됩니다.  

단, N가 소수인 경우 i로 나누어 떨어질 수 없기 때문에 for문이 끝난 뒤 자기 자신으로 남아있을 것입니다.  

### 정답코드  

```cpp
#include <bits/stdc++.h>
using namespace std;

using ll = long long;
using pii = pair<int, int>;

const int MAX = 1000001;

int n, m;

int main()
{
    //freopen("input.txt", "r", stdin);
    ios_base::sync_with_stdio(0); cin.tie(0);
    cin >> n;
    int temp = n;
    for (int i = 2; i*i <= n; i++) {
        while (temp % i == 0) {
            temp /= i;
            cout << i << "\n";
        }
    }
    if (temp != 1) {
        cout << temp;
    }
    return 0;
}

```

## N!에 p가 몇 번 곱해져 있는가?

[문제링크](https://www.acmicpc.net/problem/2004)  

### 첫 번째 풀이 : 정수론

### 알고리즘

1~n에 2의 배수는 n/2개만큼 있습니다.  
1~n에 3의 배수는 n/3개만큼 있습니다.  
1~n에 p의 배수는 n/p개만큼 있습니다.  

아래의 표처럼 생각했을 때, O의 갯수를 가로로 세면 10!에는 2가 총 $10/2^1 + 10/2^2 + 10/2^3$번 곱해져 있습니다. 

```
N   1    2    3    4    5    6    7    8    9    10
2^1      O         O         O         O          O
2^2                O                   O           
2^3                                    O           
```

일반화 해보면 n!에는 p가 총 $n/p^1 + n/p^2 + n/p^3 + ... (단, p >= n^k)$개 있습니다. 

### 정답코드

조합의 정의를 펙토리얼로 바꾸고, 펙토리얼에서 p가 몇 번등장하는지 구하면 됩니다. 2와 5 중 적게 등장한 횟수만큼 0이 만들어집니다.  

```cpp
#include <bits/stdc++.h>
using namespace std;

using ll = long long;
using pii = pair<int, int>;

const int MAX = 1000001;

ll n, m;

ll count(ll a, ll b) {
    ll mod = b;
    ll ans = 0;
    while (a >= mod) {
        ans += a / mod;
        mod *= b;
    }
    return ans;
}

int main()
{
    //freopen("input.txt", "r", stdin);
    ios_base::sync_with_stdio(0); cin.tie(0);
    cin >> n >> m;
    ll a = count(n, 2) - count(n - m, 2) - count(m, 2);
    ll b = count(n, 5) - count(n - m, 5) - count(m, 5);
    cout << min(a, b);
    return 0;
}

```

## 에라토스테네스의 체

[문제링크](https://www.acmicpc.net/problem/2004)  

### 첫 번째 풀이 : 정수론

### 알고리즘

2를 처음 만나면 2초과 2의 배수는 모두 소수가 아닙니다. 이것을 판단할 때 j는 i\*i로 시작합니다. $i * (i-1)$은 i보다 작은 i-1을 만났을 때 이미 처리가 되었을 것입니다. 따라서 j는 i * i부터 시작합니다.  

50만개의 소수를 맞을 수 (있어 보이는) 큰 수의 배열에 isPrime을 설정해두고, 처음부터 소수의 갯수를 세는 방식으로 접근합니다.  

### 정답 코드

```cpp
#include <iostream>
#include <string.h>
#include <algorithm>
using namespace std;

int n = 0;

bool isPrime[10000001];

int main(void) {
    memset(isPrime, true, sizeof(isPrime));
    isPrime[1] = false;
    // 10000000까지 소수인지 아닌지 판단
    for (int curr = 2; curr * curr <= 10000000; curr++) { // curr : 10000000의 약수 후보
        if (isPrime[curr]) {
            for (int next = curr * curr; next <= 10000000; next += curr) {
                isPrime[next] = false;
            }
        }
    }
    cin >> n;
    int ans = 0;
    for (int i = 2; i <= 10000000; i++) {
        if (isPrime[i]) {
            ans++;
            if (ans == n) {
                cout << i << "\n";
            }
        }
    }
    return 0;
}
```

## 분할정복 a^b % p

### 알고리즘 

```cpp
ll ans, p;
ll recur(int a, int b) { // 분할정복! a^b % p 구하기
    ll ret;
    if (b == 0) return 1;

    ret = recur(a, b / 2);
    ret *= ret;
    ret %= p;

    if (b % 2 == 0) return ret; // 3^16 = 3^8 * 3^8
    else return (ret * a) % p; // 3^17 = 3^8 * 3^8 * 3
}
```

**Success Notice:**
수고하셨습니다. :+1:
{: .notice--success}