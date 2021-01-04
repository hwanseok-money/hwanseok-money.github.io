---
title: "[이론] 쉽게 정리한 나머지 연산(%, modulo)"
excerpt: ""
date: 2021-01-04
last_modified_at: 
categories:
  - Algorithm
tags:
  - Algorithm
  - Theory
  - Modulo
  - MOD
  - "1000000007"
  - "1e9+7"
  - "1e9+9"
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

## 모듈러 연산

a%b는 a를 b로 나눈 나머지를 구하는 연산으로 $0~b-1$의 범위를 갖습니다.  

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
int main()
{
  //freopen("input.txt", "r", stdin);
  ios_base::sync_with_stdio(0); cin.tie(0);
  
  // a, b > 0
  cout << 17 % 5 << '\n'; // 2
  cout << 7 % 11 << '\n'; // 7
  cout << 20 % 3 << '\n'; // 2
  cout << 11 % 11 << '\n'; // 0
  
  // a < 0, b > 0
  // result = a%b;
  // result = result < 0 ? result + b : result;
  cout << -3 % 11 << "\n"; // -3
  cout << -1 % 11 << "\n"; // -1
  cout << -25 % 5 << "\n"; // 0
  cout << -11 % 11 << "\n"; // 0

  // a, b < 0
  // 모두 양수인 경우와 같다.
  cout << 17 % -5 << '\n'; // 2
  cout << 7 % -11 << '\n'; // 7
  cout << 20 % -3 << '\n'; // 2
  cout << 11 % -11 << '\n'; // 0

  return 0;
}
```

### 모듈러 연산의 특징

1. $(a + b)\ mod\ n\ = ((a\ mod\ n) + (b\ mod\ n))\ mod\ n$
  > $a = n * x_{1} + k$  
  > $b = n * x_{2} + k$  
  > $a + b = n * (x_{1} + x_{2}) + 2 * k$  
  > $(a+b)\ mod\ n = 2*k$  
  > $(a\ mod\ n) + (b\ mod\ n) = k + k = 2 * k$  
1. $(a - b)\ mod\ n\ = ((a\ mod\ n) - (b\ mod\ n))\ mod\ n$
  > $a = n * x_{1} + k$  
  > $b = n * x_{2} + k$  
  > $a - b = n * (x_{1} - x_{2})$  
  > $(a-b)\ mod\ n = 0$  
  > $(a\ mod\ n) - (b\ mod\ n) = 0$  
1. $(a * b)\ mod\ n\ = ((a\ mod\ n) * (b\ mod\ n))\ mod\ n$
  > $a = n * x_{1} + k$  
  > $b = n * x_{2} + k$  
  > $a * b = n^2(x_{1} + x_{2}) + kn(x_{1}+x_{2}) + k^2$   
  > $(a * b)\ mod\ n = k^2$  
  > $(a\ mod\ n) * (b\ mod\ n) = k * k = k^2$  
1. 나누기는 정의되지 않고, 대신 `Modular multiplicative inverse`를 사용해서 나눗셈을 곱셈으로 바꿀 수 있습니다. 이를 이해하기 위해서는 먼저 `모듈러 합동`을 이해해야 합니다.  

## 모듈러 합동(Modulo Congruent)

a와 b를 n으로 나누었을 때 나머지가 같으면 a와 b는 n에 대해서 모듈러 합동 관계이고 아래와 같이 표기합니다.    

$a \equiv b (mod\ n)$  

### 모듈러 합동의 특징 

1. a와 b가 n에 대해서 모듈러 합동 관계일 때, $a-b$는 n의 배수입니다.
  > $a = n * x_{1} + k$  
  > $b = n * x_{2} + k$  
  > $a-b = n * (x_{1} - x_{2})$  
2. $a \equiv b (mod\ n)\ \to\ b \equiv a (mod\ n)$ 
  > $a = n * x_{1} + k$  
  > $b = n * x_{2} + k$  
  > $a-b = n * (x_{1} - x_{2})$  
  > $b-a = n * (x_{2} - x_{1})$  
3. $a \equiv b (mod\ n)\ \cap\ b \equiv c (mod\ n)\ \to\ a \equiv c (mod\ n)$
  > $a = n * x_{1} + k$  
  > $b = n * x_{2} + k$  
  > $c = n * x_{3} + k$  
  > $a-b = n * (x_{1} - x_{2})$  
  > $b-c = n * (x_{2} - x_{3})$  
  > $a-c = n * (x_{1} - x_{3})$  

## 모듈러 곱셈의 역원(Modular multiplicative inverse)

나머지 연산에 대한 a의 곱셈의 역원은 수학적으로 아래와 같이 [정의](https://en.wikipedia.org/wiki/Modular_multiplicative_inverse)됩니다.  


>a modular multiplicative inverse of an integer a is an integer x such that the product ax is congruent to 1 with respect to the modulus m.

$a * x \equiv 1\ (mod\ m)$  

또한 x의 값을 알고 있다면 다음과 같은 특징을 가지고 있습니다.

$\frac{1}{a} mod\ m \to x\ mod\ m$

즉, 모듈러 연산에서 a의 역수를 a의 곱셈의 역원으로 바꾸어도 결과가 같습니다. (저는 수학자가 아니기 때문에 이 부분은 추가적인 설명 및 증명 없이 받아들이고 넘너가겠습니다.)  

### 첫 번째 풀이 : 브루트 포스

a=3, m=11일 때 m에 대한 a의 역원 중 최소값은??  
a=10, m=17일 때 m에 대한 a의 역원 중 최소값은??  

$3 * x \equiv 1\ (mod\ 11)$  
$10 * x \equiv 1\ (mod\ 17)$  

```cpp
//입력
2
3 11
10 17
```

```cpp
//출력
4
12
```

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

int getInverse(int a, int m) {
  // 모듈러 연산의 곱셈의 특징 적용
  a %= m;
	for (int x = 1; x < m; x++) {
    // *와 %의 연산자 우선순위는 동일하다. 앞에서부터 연산된다.
		if (a * x % m == 1) {
			return x;
		}
	}
}

int main()
{
	//freopen("input.txt", "r", stdin);
	ios_base::sync_with_stdio(0); cin.tie(0);
	int tc;
	cin >> tc;
	while (tc--) {
		int a, m;
		cin >> a >> m;
		cout << getInverse(a, m) << "\n";
	}
	return 0;
}
```

### 두 번째 풀이 : 확장 유클리드 알고리즘

유클리드 알고리즘은 두 수의 최대 공약수를 빠르게 찾는 방법입니다. 유클리드 알고리즘에 대한 내용은 [여기](https://hwanseok-dev.github.io/posts/algorithm/theory-euclidean-algorithm/)에 정리되어 있습니다.    


확장 유클리드 알고리즘은 아래의 식에서 a,b가 주어졌을 때 $gcd(a,b)$와 x,y를 찾는 방법입니다.    

$ax + by = gcd(a,b)$   

확장 유클리드 알고리즘에 대한 자세한 설명과 방법은 [여기](https://hwanseok-dev.github.io/posts/algorithm/extended-euclidean/)에 정리가 되어 있습니다. 본 포스팅에서는 확장 유클리드 알고리즘으로 모듈러 곱셈의 역원을 구하는 방법에 집중하겠습니다.  

먼저 확장 유클리드 알고리즘의 조건에 따라 a,b는 서로소입니다. 따라서 $gcd(a,b)$는 1입니다.

$ax + by = 1$  

위 식을 우리가 관심있는 $a * x \equiv 1\ (mod\ m)$ 식으로 변형해보겠습니다.  

> $ax + my = 1$  // 변수를 b에서 m으로 바꾸어줍니다.  
> $ax + my \simeq 1 (mod\ m)$  // 양 변에 m으로 모듈러 연산을 하면
> $ax \simeq\ 1 (mod\ m)$  // 우리가 관심있는 식이 됩니다. 

즉, 확장 유클리디안 알고리즘을 통해서 곱셈의 역원을 구할 수 있다는 것입니다. gcdExtended()은 gcd를 구해주는 함수라고 생각하고 modInverse()의 역할에 집중해서 확인합니다.  

```cpp
//출처 : https://www.geeksforgeeks.org/multiplicative-inverse-under-modulo-m/
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

// C function for extended Euclidean Algorithm 
int gcdExtended(int a, int b, int* x, int* y)
{
    // Base Case 
    if (a == 0)
    {
        *x = 0, * y = 1;
        return b;
    }

    int x1, y1; // To store results of recursive call 
    int gcd = gcdExtended(b % a, a, &x1, &y1);

    // Update x and y using results of recursive 
    // call 
    *x = y1 - (b / a) * x1;
    *y = x1;

    return gcd;
}

// Function to find modulo inverse of a 
void modInverse(int a, int m)
{
    int x, y;
    int gcd = gcdExtended(a, m, &x, &y); // 
    if (gcd != 1)
        printf("Inverse doesn't exist");
    else
    {
        // m is added to handle negative x 
        int res = (x % m + m) % m;
        printf("Modular multiplicative inverse is %d\n", res);
    }
}

int main()
{
	//freopen("input.txt", "r", stdin);
	ios_base::sync_with_stdio(0); cin.tie(0);
	int tc;
	cin >> tc;
	while (tc--) {
		int a, m;
		cin >> a >> m;
        modInverse(a, m);
	}
	return 0;
}
```

## 결론

**Success Notice:**
수고하셨습니다. :+1:
{: .notice--success}

## Reference

- <https://www.crocus.co.kr/1231>
- <https://ko.khanacademy.org/computing/computer-science/cryptography/modarithmetic/a/modular-exponentiation>
- <https://ohgym.tistory.com/13>
- <https://en.wikipedia.org/wiki/Modular_multiplicative_inverse>
- <https://www.geeksforgeeks.org/multiplicative-inverse-under-modulo-m/>