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

### 회고, 시간 초과 풀이

w와 h가 매우 큰 2의 제곱수일 때 아래의 코드는 시간초과입니다.  

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

### 개선코드

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

### 회고, 정답이긴 하지만 개선할 여지가 많았던 코드

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

### 개선 코드

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

### 알고리즘

다이내믹 프로그래밍 문제입니다.  

- dp[i] : i번까지 왔을 때, 얻을 수 있는 최대 점수
- dp[i + a[i]] = max(dp[i + ai] , dp[i] + a[i])

### 회고, 정답이지만 개선점이 많은 코드

각 인덱스에서 시작했을 때 얻을 수 있는 최대 점수를 구하는 과정을 반복했습니다. 0번째 인덱스에서 시작해서 끝까지 점프하면서 최대 점수를 갱신합니다. 1번째 인덱스에서 같은 과정을 수행할 때, 0번째 인덱스에서 방문했던 지점에 대해 아래의 공식을 적용했습니다.  

- dp[i] : i번까지 왔을 때, 얻을 수 있는 최대 점수
- for all i, dp[i] = v[i] and then, dp[i+v[i]] = dp[i] + v[i]

우선 dp[i] = v[i]를 적용했습니다. dp[0] = v[0]이기도 하고, 이렇게 해두면 dp[i + v[i]] = dp[i] + v[i]의 공식을 사용할 수 있습니다. jump를 사용한 누적합의 개념입니다.  

| - || 1 | 2 | 3 | 4 | 5 |
|:--|:--|:--|:--|:--|:--|
|v[i]| 1 | 2 | 3 | 4 | 5 |
|dp[i]| 1 | 3 | 3 | 7 | 15 |

1. memset에서 sizeof를 사용하지 않았습니다.
1. dp[i + ai] = max(dp[i + ai] , dp[i] + ai)의 식은 파악했지만, 이게 다이나믹 프로그래밍 문제라고 생각하지는 못했습니다. 위와 같이 dp[i]를 정의하고 사용하기 때문에 dp 문제입니다.  
  > DP의 두가지 속성Permalink
  > Overlapping Subproblem : 부분 문제가 겹친다. 부분 문제를 여러번 구해야하는 경우가 발생한다.
  > Optiaml Substructure : 부분 문제의 정답이 항상 같다. 작은 동일한 문제가 나오면 이 두 문제의 정답은 항상 같아야 한다. 따라서 부분 문제의 값을 저장해어서 실행시간을 줄인다.
1. 자주 사용하는 값에 대해서 변수를 선언해서 가독성을 높이지 않았습니다.( i + a[i] )
  ```cpp
  while (i <= n) {
    int next = i + a[i];
    if (next > n) break;
    if (dp[i] + a[next] > dp[next]) {
        dp[next] += dp[i];
        ans = max(ans, dp[next]);
    }
    else {
        break;
    }
    i = next;
  }
  ```  

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

int a[200010];
int dp[200010];

int main()
{
  //freopen("input.txt", "r", stdin);
  ios_base::sync_with_stdio(0); cin.tie(0);
  int tc = 0; cin >> tc;
  while (tc--) {
    int n = 0; cin >> n;
    memset(a, 0, 200010);
    memset(dp, 0, 200010);
    int ans = 0;
    for (int i =1; i <=n; i++) {
      cin >> a[i];
      dp[i] = a[i];
      ans = max(ans, a[i]);
    }

    for (int j = 1; j <= n; j++) {
      int i = j;
      while (i <= n) {
        if (i + a[i] > n) break;
        // 현재까지 + 다음칸 <= 이미 방문한 칸
        // 안가도 되면
        if (dp[i] + a[i + a[i]] > dp[i + a[i]]) {
          dp[i + a[i]] += dp[i];
          ans = max(ans, dp[i + a[i]]);
        }
        else {
          break;
        }
        i += a[i];
      }
    }
    cout << ans << "\n";
  }
  return 0;
}
```

### 개선된 풀이

개선된 풀이 1은 실행시간 170ms로 통과, 개선된 풀이 2는 139ms로 통과했습니다.  

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

int a[200010];
int dp[200010];

int main()
{
    //freopen("input.txt", "r", stdin);
    ios_base::sync_with_stdio(0); cin.tie(0);
    int tc = 0; cin >> tc;
    while (tc--) {
        int n = 0; cin >> n;
        memset(a, 0, size(a));
        memset(dp, 0, size(dp));
        int ans = 0;
        for (int i = 1; i <= n; i++) {
            cin >> a[i];
            dp[i] = a[i];
            ans = max(ans, a[i]);
        }

        for (int j = 1; j <= n; j++) {
            int i = j;
            while (i <= n) {
                int next = i + a[i];
                if (next > n) break;
                if (dp[i] + a[next] > dp[next]) {
                    dp[next] += dp[i];
                    ans = max(ans, dp[next]);
                }
                else {
                    break;
                }
                i = next;
            }
        }
        cout << ans << "\n";
    }
    return 0;
}
```

### 개선된 풀이 2

개선된 풀이 1은 실행시간 170ms로 통과, 개선된 풀이 2는 139ms로 통과했습니다.  

각 인덱스에서 시작했을 때 얻을 수 있는 최대 점수를 구하는 과정을 반복하지 않는 방법입니다. 각 인덱스에서 바로 다음 인덱스에 대한 dp[i+v[i]]만 갱신합니다.  

최대 값을 구하기 위해서는 어땠든 모든 jump는 확인되어야 하기 때문에 이 방법으로도 정답이 구해집니다. 물론 각 인덱스에 대해서 바로 다음만 신경쓰기 때문에 코드가 간결합니다. 그리고 다음 jump가 범위를 벗어날 때만 최대값을 갱신해주면 됩니다.  


```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

int v[200010];
int dp[200010];

int main()
{
    //freopen("input.txt", "r", stdin);
    ios_base::sync_with_stdio(0); cin.tie(0);
    int tc = 0; cin >> tc;
    while (tc--) {
        int n = 0; cin >> n;
        memset(v, 0, size(v));
        memset(dp, 0, size(dp));
        int ans = 0;
        for (int i = 1; i <= n; i++) {
            cin >> v[i];
            // 중요!
            dp[i] = v[i];
            ans = max(ans, v[i]);
        }
        // dp[i] : i번째까지 방문했을 때 얻을 수 있는 최대 점수(v[i] 포함)
        for (int i = 1; i <= n; i++) {
            int next = i + v[i];
            // 다음 인덱스가 범위를 벗어나면 
            if (next > n) ans = max(ans, dp[i]);
            else dp[next] = max(dp[next], dp[i] + v[next]);
        }
        cout << ans << "\n";
    }
    return 0;
}
```

## D. Even-Odd Game

### 알고리즘  

sample input의 두 번째 케이스가 Tie가 나온는 이유를 파악해야 합니다. 3 2 1이 주어졌을 때 A는 3을 가져갑니다. 2를 가져가서 자신이 2점을 얻는 것보다 B가 3점을 얻지 못하도록 하는 것이 더 이득이기 때문입니다. 마찬가지로 B는 2점을, A는 1점을 가져가서 둘 다 0점으로 Tie 게임이 됩니다.  

이처럼 가장 큰 값을 가져가되, 자신의 점수에 포한된는지 여부를 따지면 됩니다.  

### 시간 초과 풀이

아래는 alice와 bob의 vector를 구분했습니다. 구분하지 않고 진행해도 됩니다. 남아있는 값 중에서 가장 큰 값을 빼야하는 점은 처음부터 끝까지 유지되니까요. 이렇게되면 문제의 정의상 priority_queue를 사용하는 것이 자료구조 선택에 최적임을 알 수 있습니다.  

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
		int n = 0;
		cin >> n;
		ll temp;
		vector<ll> alice;
		vector<ll> bob;
		ll sum_a = 0, sum_b = 0;
		for (int i = 0; i < n; i++) {
			cin >> temp;
			if (temp % 2 == 0) {
				alice.push_back(temp);
			}
			else {
				bob.push_back(temp);
			}
		}
		sort(alice.begin(), alice.end(), std::greater<int>());
		sort(bob.begin(), bob.end(), std::greater<int>());
		
		for (int i = 0; i < n; i++) {
			ll top = 0;
			if (!alice.empty() && !bob.empty()) {
				if (alice[0] > bob[0]) {
					top = alice[0];
					alice.erase(alice.begin());
				}
				else {
					top = bob[0];
					bob.erase(bob.begin());
				}
			}
			else if (!alice.empty()) {
				top = alice[0];
				alice.erase(alice.begin());
			}
			else if (!bob.empty()) {
				top = bob[0];
				bob.erase(bob.begin());
			}
			if (i % 2 == 0 && top % 2 == 0) {
				sum_a += top;
			}
			else if (i % 2 == 1 && top % 2 == 1) {
				sum_b += top;
			}
		}
		if (sum_a > sum_b) cout << "Alice\n";
		else if (sum_a < sum_b) cout << "Bob\n";
		else cout << "Tie\n";
	}
	return 0;
}
```

### 개선된 풀이 

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
		int n = 0;
		cin >> n;
		ll temp;
		priority_queue<ll, vector<ll>> pq;
		ll sum_a = 0, sum_b = 0;
		for (int i = 0; i < n; i++) {
			cin >> temp;
			pq.push(temp);
		}
		for (int i = 0; i < n; i++) {
			ll top = pq.top();
			pq.pop();
			if (i % 2 == 0 && top % 2 == 0) {
				sum_a += top;
			}
			else if (i % 2 == 1 && top % 2 == 1) {
				sum_b += top;
			}
		}
		if (sum_a > sum_b) cout << "Alice\n";
		else if (sum_a < sum_b) cout << "Bob\n";
		else cout << "Tie\n";
	}
	return 0;
}
```

### 더 개선된 풀이

생각을 해보니 값을 pop()하지 않아도 됩니다.  

```cpp
#include<bits/stdc++.h>
using namespace std;
 
typedef long long ll;
 
int main()
{
	ios_base::sync_with_stdio(0); cin.tie(0);
	int t; cin >> t;
	while (t--){
		int n; cin >> n;
		vector<ll>v(n);
		for (int i = 0; i < n; i++) cin >> v[i];
		sort(v.begin(), v.end(), greater<int>());
 
		ll sum1 = 0, sum2 = 0;
		for (int i = 0; i < n; i++) {
			if (i % 2 == 0 && v[i] % 2 == 0) sum1 += v[i];
			else if (i % 2 == 1 && v[i] % 2 == 1) sum2 += v[i];
		}
		if (sum1 > sum2) cout << "Alice\n";
		else if (sum1 < sum2) cout << "Bob\n";
		else cout << "Tie\n";
	}
	return 0;
}
```

## E. Correct Placement

### 알고리즘

기본적으로는 모든 쌍을 확인하면서 조건을 만족하는지 확인하면 됩니다. 다만, 완전탐색으로 진행하면 $4 * 10^10$으로 4초의 시간제한을 초과합니다. 따라서 정렬을 해서 비교를 덜 할 수 있는 방법을 찾는 것이 핵심입니다.  



### 시간제한 풀이

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
		int n = 0;
		cin >> n;
		vector<pair<int, int> > v(n);
		for (int i = 0; i < n; i++) {
			cin >> v[i].first >> v[i].second;
		}
		for (int i = 0; i < n; i++) {
			bool flag = false;
			for (int j = 0; j < n; j++) {
				if (i == j) continue;
				if ((v[j].first < v[i].first && v[j].second < v[i].second) ||
					(v[j].second < v[i].first && v[j].first < v[i].second)) {
					cout << j+1 << " ";
					flag = true;
					break;
				}
			}
			if (!flag) {
				cout << -1 << " ";
			}
		}
		cout << "\n";
	}
	return 0;
}
```

### 개선된 풀이 

## F. New Year's Puzzle

풀지 못했습니다. :worried: 
 
## G. Moving to the Capital

풀지 못했습니다. :worried: 

