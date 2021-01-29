---
title: "[Contest] Codeforces Round #695 (Div.2)"
excerpt: ""
date: 2021-01-08
last_modified_at: 
categories:
  - Contest
tags:
  - Contest
  - Codeforces
  - "#693"
  - Wizard of Orz
  - Hills And Valleys
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: false
---

## 문제 링크

[문제링크](https://codeforces.com/contest/1467) 

## A. Wizard of Orz

가장 큰 값을 구해야하기 때문에 왼쪽의 숫자가 가장 크도록 만들어야 합니다. 결국 첫 번째 숫자는 9로 고정입니다.  

- 1 자리 수, 1 번째 자리에서 stop을 하면 9
- 2 자리 수, 2 번째 자리에서 stop을 하면 98
- 3 자리 수, 3 번째 자리에서 stop을 하면 987
- 3 자리 수, 2 번째 자리에서 stop을 하면 989
- 4 자리 수, 3 번째 자리에서 stop을 하면 9878
- 4 자리 수, 2 번째 자리에서 stop을 하면 9890

따라서 세 번째 자리 이하에서 멈출수록 값이 더 작아집니다. 멈추는 자리는 2번째가 최적이니 출력되는 수는 989'0123456789'0123456789'...에서 앞에서 n자리일 것입니다.  

### 알고리즘

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
        int n = 0; cin >> n;
        if (n == 1)cout << "9\n";
        else if (n == 2) cout << "98\n";
        else if (n == 3) cout << "989\n";
        else {
            cout << "989";
            for (int i = 0; i < n - 3; i++) {
                cout << i % 10;
            }
            cout << "\n";
        }
    }
    return 0;
}
```

## B. Hills And Valleys

### 알고리즘  

가장 왼쪽과 가장 오른쪽은 첨점이 될 수 없습니다. 첨점을 판단하는 함수를 하나 만들고 이를 사용합니다.  

첨점을 이루는 3개의 점중 가운데 점을 왼쪽/오른쪽에 일치시켜봅니다. 값을 변경하기 전보다 첨점이 줄어들거나 많아질 수 있습니다.  

값을 변경했다가 다시 되돌리는 과정이 필수적입니다.  

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
 
int n = 0;
const int MAX = 200010;
vector<int> v;
vector<bool> sharp;
bool isSharp(int i) {
    if (i == 0 || i == n - 1) return false;
    if ((v[i - 1] < v[i] && v[i] > v[i + 1]) ||
        (v[i - 1] > v[i] && v[i] < v[i + 1])) return true;
    return false;
}
 
int main()
{
    //freopen("input.txt", "r", stdin);
    ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0);
    int tc = 0; cin >> tc;
    while (tc--) {
        n = 0; cin >> n;
        v = vector<int>(n, 0);
        sharp = vector<bool>(n, false);
        int a;
        for (int i = 0; i < n; i++) {
            cin >> v[i];
        }
        int ans = 0;
        for (int i = 1; i < n - 1; i++) {
            if (isSharp(i)) sharp[i] = true, ans++;
        }
        int diff = 0;
        for (int i = 1; i < n - 1; i++) {
            if (sharp[i]) {
                int before = sharp[i - 1] + sharp[i] + sharp[i + 1];
                int save = v[i];
                v[i] = v[i - 1];
                int after = isSharp(i - 1) + isSharp(i) + isSharp(i + 1);
                // abs(before- after)이라고 하면 첨점이 더 생기는 경우를 찾지 못한다.
                diff = max(diff, before - after);
 
                v[i] = v[i + 1];
                after = isSharp(i - 1) + isSharp(i) + isSharp(i + 1);
                diff = max(diff, before - after);
                // 바꾸기 전 값으로 되돌려준다. 
                v[i] = save;
            }
        }
        cout << ans - diff << "\n";
    }
    return 0;
}
```