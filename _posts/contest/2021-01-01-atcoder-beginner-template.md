---
title: "[Contest] AtCoder Beginner Contest 187"
excerpt: ""
date: 2021-01-03
last_modified_at: 
categories:
  - Contest
tags:
  - Contest
  - Atcodere
  - Beginner
  - "187"
  - Large Digits
  - Gentle Pairs
  - 1-SAT
  - Choose Me
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: false
---

## 문제 링크

[문제링크](https://atcoder.jp/contests/abc187/tasks) 

## A.	Large Digits

### 알고리즘

Input을 string으로 받아서 index로 각각에 접근하여 해결할 수 있습니다. 

### 정답 코드

```cpp
#include <iostream>

using namespace std;

int foo(string a, string b) {
  int A = 0;
  int B = 0;

  for (int i = 0; i < a.size(); i++) {
    A += a[a.size() - i - 1] - '0';
    B += b[b.size() - i - 1] - '0';
  }

  if (A < B) return B;
  else return A;
}

int main(void) {
  //freopen("input.txt", "r", stdin);

  string a, b;

  cin >> a >> b;
  cout << foo(a, b);

  return 0;
}
```

## B.	Gentle Pairs

### 알고리즘

입력으로 주어지는 N개의 점 중 2개를 고르고, 이 점의 기울기의 절대값이 1이하인지 판단하는 문제입니다. N이 1e3까지 이므로 O(N^2)으로 풀 수 있습니다. 비록 입력으로 주어지는 값이 int라고 명시되어 있어도, 기울기를 구할 때 나누기 연산을 하기 때문에 double을 사용해야합니다. 입력을 저장할 배열을 만들때 double을 사용해도 되고, int 배열에 저장한 뒤, 나누기 연산을 하기 전에 double로 형변환을 해도 됩니다.  

### 정답 코드

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
#include <cstring>
#define MAX 1010

using namespace std;

double point[MAX][2];

int main(void) {
  //freopen("input.txt", "r", stdin);

  int n = 0;
  cin >> n;
  int a, b, ans = 0;
  for (int i = 0; i < n; i++) {
    cin >> point[i][0] >> point[i][1];
  }

  for (int i = 0; i < n; i++) {
    for (int j = i + 1; j < n; j++) {
      double x = (point[j][1] - point[i][1]) / (point[j][0] - point[i][0]);
      if (-1.0 <= x && x <= 1.0) {
        ans++;
      }
    }
  }
  cout << ans;
  return 0;
}
```

## C.	1-SAT

### 알고리즘

N개의 문자열이 주어지고, 각각의 문자열은 공백이 없는 소문자로 구성되어 있습니다. 각각의 문자열의 시작에는 '!' 문자가 있을 수도 있고, 없을 수도 있습니다. 어떤 문자 T는 다음의 조건을 만족할 때 `unstisfied`입니다.

- T의 시작 부분에 '!'를 붙이는 것과 상관없이(regardless of whether we add an ! at the beginning of T) S1, S2, ... , Sn 문자 중 어떤 하나와도 일치한다.

위 조건을 풀어서 적으면 다음의 두 가지를 **모두** 만족하는 문자 T를 찾으라는 말입니다.  

1. T가 '!'로 시작할 때는 T에서 '!'를 제외한 문자열이 S1, ... , Sn에 있다.
1. T가 '!'로 시작하지 않을 때 T에서 '!'를 추가한 문자열이 S1, ... , Sn에 있다.

아래의 Sample Input 1에 대해서, 

```
6
a
!a
b
!c
d
!d
```

우선 T는 S1, ... , Sn의 범위에서만 고려해야합니다. 제일 먼저 a가 unsatisfied인지 판단해보겠습니다. a는 그 자체로 S1이기 때문에 `조건 1`을 만족합니다. 그리고 "!a"는 S2로서 범위 안에 존재하기 때문에 a는 unsatisfied입니다.  

만약 Sample Input이 아래와 같이 주어졌다면,

```
6
a
!a
b
!c
d
!d
```

그래도 "!a"가 아닌 "a"를 출력해야합니다. "!a"는 시작 부분에 0~1개의 '!'를 붙이면 {"!a","!!a"}가 되고 "!!a"는 범위에 없기 때무에 "!a"는 unsatisfied가 될 수 없습니다. 

### 시간 초과 코드

O(N^2)로 접근하는 방법은 TC 30개 중 19개 정답, 11개 시간 초과입니다.
O((2 * 10^5) * (2 * 10^5) * 10(문자의 최대 길이) )이기 때문에 O(10^11)입니다. 약 1억번(1e8)의 연산이 1초라는 것을 생각해볼 때 시간초과가 당연합니다.  

```cpp
#include <bits/stdc++.h>
using namespace std;


int main(void) {
  //freopen("input.txt", "r", stdin);

  int n = 0;
  cin >> n;
  vector<string> v(n);
  for (int i = 0; i < n; i++) {
    cin >> v[i];
  }

  for (int i = 0; i < n; i++) {
    // satisfied인지 판단할 문자열
    string curr = v[i];
    for (int j = i+1; j < n; j++) {
      if (curr[0] == '!') {
        // 나머지가 curr.substr(1)과 같은지 확인
        if (v[j].compare(curr.substr(1, curr.size())) == 0) {
          cout << curr.substr(1, curr.size()) << "\n";
          return 0;
        }
      }
      else {
        // 나머지가 '1'+curr과 같은지 확인
        if (v[j].compare('!' + curr) == 0) {
          cout << curr << "\n";
          return 0;
        }
      }
    }
  }
  cout << "satisfiable";
  return 0;
}
```

### 정답 코드

문자열 집합에 특정 문자가 존재하는지 판단하기 위해서 map을 사용합니다. 내부적으로 해시를 사용하기 때문에 O(1)시간 만에 찾을 수 있습니다.  

```cpp
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
int main()
{
  //freopen("input.txt", "r", stdin);

  ios_base::sync_with_stdio(0); cin.tie(0);
  int n; cin >> n;
  vector<string> v(n);
  for (int i = 0; i < n; i++) cin >> v[i];
  map<string, int> mp;
  for (int i = 0; i < n; i++) {
    // unsatisfied인지 판단할 문자
    string curr = v[i];
    if (curr[0] == '!') {
      // '!'로 시작하면 '!'가 없는 문자열 찾기
      if (mp.count(curr.substr(1, curr.size()))) {
        cout << curr.substr(1, curr.size()) << "\n";
        return 0;
      }
    }
    else {
      // '!'로 시작하지 않으면 '!'가 추가된 문자열 찾기
      if (mp.count('!' + curr)) {
        cout << curr << "\n";
        return 0;
      }
    }
    // 현재까지 확인한 문자열만으로 unsatisfied라고 판단되지 않은 문자열은 모두 추가
    mp[curr]++;
  }
  cout << "satisfiable\n";
  return 0;
}
```

## D.	Choose Me

### 알고리즘

N개의 마을이 있고 A 지지자와 B 지지자가 있습니다. B가 어떤 마을에서 연설을 하면 그 마을의 모든 지지자가 B에게 투표합니다. 대신 B가 연설을 하지 않은 마을은 A지지자만 투표하고 B 지지자는 투표하지 않습니다.  

마을이 10^5개가 있고, 각 마을의 지지자가 10^9명까지 존재할 수 있기 때문에 전체 선거에서 총 득표수를 따지기 위해서는 long long을 사용해야 합니다. int는 +-21억까지 저장 가능하기 때문입니다.  

만약 B가 연설을 하지 않고 가만히 있을 때 A는 모든 마을의 모든 A 지지자의 합만큼 득표를 하게 됩니다. 그리고 B가 마을에서 연설을 할 때마다, A는 해당 마을의 A 지지자만큼 표를 잃고, B는 마을의 모든 투표자 수만큼 표를 얻습니다. 

우선 Sample Input1를 가지고 Greedy하게 생각해보겠습니다. 어떤 마을에서 연설을 하면 A와 B의 표를 모두 가져올 수 있기 때문에 A+B의 표가 많은 곳에서 연설하는 것이 좋습니다. 만약 A+B가 같은 경우 A가 표를 많이 잃도록 하는 것이 좋기 때문에 A의 지지자가 많은 순서대로 연설하는 것이 좋아보입니다. 

```
4 // # of test case
2 1 // A지지자 B지지자
2 2
5 1
1 3
```

| A | B | A + B |우선순위에 따라 연설 했을 때 얻을 수 있는 표(A/B)
|:--|:--|:------|:------|
| 2 | 1 | 3 | 0/17 |
| 1 | 3 | 4 | 2/14 |
| 2 | 2 | 4 | 3/10(4,3번째 마을에서 연설한 경우) |
| 5 | 1 | 6 | 5/6(4번째 마을에서 연설한 경우) |

그런데 아래의 경우에서는 Greedy한 접근이 틀린 결과를 냅니다.

```
3 // # of test case
1 4
3 1
2 0
```

| A | B | A + B |우선순위에 따라 연설 했을 때 얻을 수 있는 표(A/B)
|:--|:--|:------|:------|
| 2 | 0 | 2 | 0/11 |
| 3 | 1 | 4 | 2/9 |
| 1 | 4 | 5 | 5/5 |

따라서 이 경우 `A+B`가 아닌 `2*A+B`로 정렬을 해야 합니다. 

| A | B | 2A + B |우선순위에 따라 연설 했을 때 얻을 수 있는 표(A/B)
|:--|:--|:------|:------|
| 2 | 0 | 4 | 0/11 |
| 1 | 4 | 6 | 2/9 |
| 3 | 1 | 7 | 3/4 |

왜 2A+B로 정렬을 해야할까요?  

(A가 얻은 표의 수) < (B가 얻은 표의 수)가 되도록 만들어야 합니다. 이 조건을 만족하게 하기 위해서는 (B가 얻은 표의 수)를 크게 만들 수도 있지만, (A가 얻은 표의 수)를 작게 만들 수도 있습니다. 당연히 두 가지 방법을 동시에 사용하면 더 효과적입니다. 그리고 B가 연설을 하는 것이 두 가지 방법을 모두 사용하는 것임을 알 수 있습니다.  

즉, B가 1번 연설을 하는 행위를 통해 (B가 얻은 표의 수)가 (A가 얻은 표의 수)보다 얼마나 더 커지는지를 생각하면 A가 잃는 표까지 생각해서 2 * A + B만큼의 이득을 얻게 됩니다. 정렬은 이득을 가장 크게 얻을 수 있는 기준에 따라 하는 것이 맞기 때문에 2A+B를 기준으로 정렬을 해야합니다. 

### 정답 코드

```cpp
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
int main()
{
  //freopen("input.txt", "r", stdin);

  ios_base::sync_with_stdio(0); cin.tie(0);
  int n; cin >> n;
  ll a_sum = 0, b_sum = 0;
  vector<tuple<ll, ll, ll> >v(n);
  for (int i = 0; i < n; i++)
  {
    ll a, b; cin >> a >> b;
    v[i] = make_tuple(2*a + b, a, b);
    a_sum += a;
  }
  sort(v.begin(), v.end());
  int ans = 0;
  for (int i = n - 1; i >= 0; i--)
  {
    ll t_sum, t_a, t_b;
    tie(t_sum, t_a, t_b) = v[i];
    b_sum += t_a + t_b;
    a_sum -= t_a;
    if (a_sum < b_sum) {
      ans = n - i;
      break;
    }
  }
  cout << ans << "\n";
  return 0;
}
```


E,F 문제는 풀지 못했습니다.  

## E.	Through Path

### 알고리즘

### 정답 코드

## F.	Close Group

### 알고리즘

### 정답 코드

**Success Notice:**
AtCoder Beginner Contest 187 문제를 풀어봤습니다. 수고하셨습니다. :+1:
{: .notice--success}


