---
title: "[Contest] Codeforces Round #693 (Div.3)"
excerpt: ""
date: 2021-01-05
last_modified_at: 
categories:
  - Contest
tags:
  - Contest
  - Codeforces
  - "#693"
  - Cards for Friends
  - Fair Division
  - Long Jumps
  - Even-Odd Game
  - Correct Placement
  - New Year's Puzzle
  - Moving to the Capital
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: false
---

## 문제 링크

[문제링크](https://codeforces.com/contest/1472) 

## A. Cards for Friends

### 알고리즘

가로와 세로가 짝수라면 반으로 나눌 수 있습니다. 가능한 많이 나누면 됩니다. 한 번 자를 때마다 종이는 2배로 증가합니다.  

> After cutting a sheet of paper, the total number of sheets of paper is increased by 1.  

한 장이 두장이 되니, 전체는 두 배가 되는게 맞습니다.  

### 시간 초과 풀이

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

int ans = 1;

void recur(int w, int h) {
	if (w % 2 == 0) {
		ans++;
		recur(w / 2, h);
		recur(w / 2, h);
	}
	else if (h % 2 == 0) {
		ans++;
		recur(w, h / 2);
		recur(w, h / 2);
	}
}

int main()
{
	//freopen("input.txt", "r", stdin);
	ios_base::sync_with_stdio(0); cin.tie(0);

	int tc = 0; cin >> tc;
	while (tc--) {
		int w, h, n;
		cin >> w >> h >> n;
		ans = 1;
		if (n == 1) {
			cout << "YES\n";
			continue;
		}
		recur(w,h);
		if (ans >= n) {
			cout << "YES\n";
		}
		else {
			cout << "NO\n";
		}
	}

	return 0;
}
```

### 정답코드

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

int main()
{
	//freopen("input.txt", "r", stdin);
	ios_base::sync_with_stdio(0); cin.tie(0);

	int tc = 0; cin >> tc;
	while (tc--) {
		int w, h, n;
		cin >> w >> h >> n;
		int ans = 1;
		
		while (w % 2 == 0) {
			w /= 2;
			ans *= 2;
		}
		while (h % 2 == 0) {
			h /= 2;
			ans *= 2;
		}

		if (ans >= n) {
			cout << "YES\n";
		}
		else {
			cout << "NO\n";
		}
	}

	return 0;
}
```

## B. Fair Division

### 알고리즘  

1g의 갯수와 2g의 갯수는 각각 홀/짝일 수 있기 때문에 4가지 경우가 존재합니다. 4 가지 경우에 대해서 일일이 따져도 되지만, 안되는 경우만 확인해서 NO를 출력하는 방향이 편합니다.  

먼저 전체 무게를 동등하게 나누어야 하는데, 전체 무게의 합이 홀수라면 불가능합니다. 이것을 if(전체 무게 %2 == 1)로 표현할게 아니라, if(1g의 갯수 % 2 == 1)이라고 표현하는 편이 좋습니다. 즉, 1g의 갯수가 홀수개면 2g의 갯수가 홀수개이든, 짝수개이든 절대 불가능합니다.  

1g의 갯수가 짝수개로 고정되었기 때문에 4가지 중 2가지만 남았습니다. 2g의 갯수가 짝수일 때는 절반으로 나누면 됩니다. 그런데 2g의 갯수가 홀수개라면 2g만 나눴을 때 한 명이 2g을 더 가져가게 됩니다. 이것을 1g으로 동등하게 만들기 위해서는 1g 2개가 필요합니다. 다시 말하지만 1g의 갯수는 짝수개이기 때문에 1g이 4개, 6개라도 상관없습니다. 2g짜리에 의한 불균현을 맞추기 위해 1g 2개를 사용하고 나머지는 절반으로 나누면 되기 때문입니다.  

정리하면 불가능한 경우는 아래와 같습니다.  

1. 1g짜리가 홀수개인 경우 모두
1. 2g짜리가 홀수개이고, 1g짜리가 2개 미안인 경우(1g짜리는 짝수개라는 가정)

### 정답이긴 하지만 개선할 여지가 많았던 코드

가능한 경우롤 4가지로 나누어서 생각하지 못했고, 안되는 경우가 아닌, 되는 경우를 생각하다보니 if의 조건이 매우 복잡합니다.  

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
int main()
{
	//freopen("input.txt", "r", stdin);
	ios_base::sync_with_stdio(0); cin.tie(0);
	int tc = 0;
	cin >> tc;
	while (tc--) {
		int n; cin >> n;
		int a = 0, b = 0;
		int c;
		int sum = 0;
		for (int i = 0; i < n; i++) {
			cin >> c;
			sum += c;
			if (c == 1) a++;
			else b++;
		}
		if (sum % 2 == 1) {
			cout << "NO\n";
			continue;
		}
		else {
			// 3. 2가 짝수개 -> 1이 짝수개
			// 4. 2가 홀수개 -> 1이 2개 이상 짝수개
			// 5. 
			if ((2 * b == sum && b % 2 == 0)||
				(a == sum)||
				(b % 2 == 0 && a % 2 == 0) ||
				(b % 2 == 1 && a >= 2 && a%2 == 0)) {
				cout << "YES\n";
			}
			else {
				cout << "NO\n";
			}
		}
	}
	return 0;
}
```

### 정답 코드

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
int main()
{
	//freopen("input.txt", "r", stdin);
	ios_base::sync_with_stdio(0); cin.tie(0);
	int tc = 0;
	cin >> tc;
	while (tc--) {
		int n; cin >> n;
		int a = 0, b = 0;
		int c;
		int sum = 0;
		for (int i = 0; i < n; i++) {
			cin >> c;
			sum += c;
			if (c == 1) a++;
			else b++;
		}
		
		if (a % 2 == 1) {
			cout << "NO\n";
		}
		else {
			if (b % 2 == 0) {
				cout << "YES\n";
			}
			else {
				if (a < 2) {
					cout << "NO\n";
				}
				else {
					cout << "YES\n";
				}
			}
		}

	}
	return 0;
}
```


## C. Long Jumps
## D. Even-Odd Game
## E. Correct Placement
## F. New Year's Puzzle
## G. Moving to the Capital
