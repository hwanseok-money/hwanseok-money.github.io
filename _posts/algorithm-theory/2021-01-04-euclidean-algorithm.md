---
title: "[이론] 쉽게 정리한 유클리드 알고리즘(유클리드 호제법)"
excerpt: ""
date: 2021-01-04
last_modified_at: 
categories:
  - Algorithm-Theory
tags:
  - Algorithm-Theory
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


##  유클리드 알고리즘

유클리드 알고리즘(= 유클리드 호제법)은 **두 정수 a,b가 서로소 관계에 있을 때** 최대공약수를 효과적으로 구하기 위한 방법입니다. 정의보다 코드가 더 쉽습니다.  

```cpp
int gcd(int a, int b)
{
  if(b==0) return a;
  return gcd(b,a%b);
}
```

$gcd(a,b) \equiv gcd(b, r)\ (단,\ a>b이고,\ a \equiv r\ (mod\ b))$  

증명은 [여기](https://baeharam.github.io/posts/algorithm/extended-euclidean/)에 잘 정리되어 있습니다.  

조건에 의해 $r$은 b에 대해 a와 모듈러 합동인 수입니다. 즉, r는 b로 나누었을 때 나머지가 a%b인 수는 모두 가능합니다. 구현을 할 때 조건을 만족하는 가장 작은 값인 a%b를 사용한 것입니다.   

## 확장 유클리드 알고리즘

확장 유클리드 알고리즘은 아래의 식에서 a,b가 주어졌을 때 $gcd(a,b)$와 x,y를 찾는 방법입니다.  

확장 유클리드 알고리즘에 대한 자세한 설명과 방법은 [여기](https://baeharam.github.io/posts/algorithm/extended-euclidean/)에 정리가 되어 있습니다.  

확장 유클리드 알고리즘을 사용해서 곱셈의 모듈러 연산을 구하는 방법은 [여기](https://hwanseok-dev.github.io/algorithm/theory-modulo/)에 정리가 되어 있습니다.  



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