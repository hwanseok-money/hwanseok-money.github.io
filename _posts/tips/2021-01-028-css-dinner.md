---
title: "[Tips] CSS selecter game : CSS Dinner"
excerpt: ""
date: 2021-01-28
categories:
  - Tips
tags:
  - Tips
  - CSS
  - CSS Dinner
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true

---


| 레벨 | 선택자 | 의미 | 정답 |
|:-----|:-----|:-----|:-----|
| 1 | `A` | 모든 \<A\> | plate |
| 2 | `A` | 모든 \<A\> | bento |
| 3 | `A#long` | \<A id="long"\> | plate#fancy |
| 4 | `A B` | 모든 \<A\>안의 \<B\>| plate apple |
| 5 | `#long B` | 모든 \<?? id="long"\>안의 \<B\> | #fancy pickle |
| 6 | `.neato` | \<?? class="neato"\> | .small |
| 7 | `A.important` | \<A class="important"\> | orange.small |
| 8 | 리마인드 | 스테이지 | bento orange.small<br/> |
| 9 | `A,B` | 모든 \<A\>와\<B\>| plate, bento |
| 10 | `*` | ALL | * |
| 11 | `A  *` | \<A\>안의 모두 | plate * |
| 12 | `A+B` | \<\A>바로 뒤의 \<B\> | plate+apple |
| 13 | `A~B` | \<\A> 뒤의 \<B\><br/>(\<A\>와 같은 레벨의 \<\B>가 아닌 태그가 나타날 때까지) | bento~pickle |
| 14 | `A>B` | Direct Child | plate>apple |
| 15 | `:first-child`<br/>`A:first-child`<br/>`A B:first-child`<br/> | 모든 첫 번째 자식<br/>A의 첫 번째 자식<br/>A 아래의 B의 첫번째 자식 | orange:first-child<br/>plate orange:first-child |
| 16 | `A:only-child`<br/>`A B:only-child`<br/> | 다른 태그의 유일한 자식인 모든 A<br> A안의, 다른 태그의 유일한 자식인 모든 B | apple,plate pickle:only-child<br/>plate apple:only-child, plate pickle:only-child |
| 17 | `:last-child`<br/>`A:last-child`<br/>`A B:last-child`<br/> | 모든 마지막 자식<br/>다른 태그의 마지막 자식인 모든 A<br> A안의, 다른 태그의 마지막 자식인 모든 B | plate apple:last-child, pickle.small |
| 18 | `:nth-child(N)`<br/>`A:nth-child(N)`<br/>`A B:nth-child(N)`<br/> | (인덱스 1부터 시작)<br/>모든 n번째 자식<br/> 다른 태그의 n번째 자식인 모든 A<br/> A안의, 다른 태그의 n번째 자식인 모든 B | plate:nth-child(3) |
| 19 | `:nth-last-child(3)`<br/>`A:nth-last-child(3)`<br/>`A B:nth-child(N)`<br/>| (인덱스 1부터 시작)<br/>모든 뒤에서 n번째 자식<br/> A 태그의 뒤에서 n번째 자식인 모든 A | bento:nth-last-child(3) |
| 20 | `A:first-of-type` | 첫 번째 등장하는  A | apple:first-of-type |
| 21 | `A:nth-of-type(n)`<br/>`A:nth-of-type(even)` | n번째 등장하는 A<br/>짝수번째 등장하는 A | plate:nth-of-type(even) |
| 22 | `A:nth-of-type(bn+c)` | c부터 시작해서 b번째의 A<br/>(In python, for _ in rangeA[c::b]) | plate:nth-of-type(2n+3) |
| 23 | `A B:only-of-type` | A안의 유일한 B | plate apple:only-of-type |
| 24 | `A:last-of-type` | 마지막에 등장하는 A | orange:last-of-type, apple:last-of-type |
| 25 | `A:empty` | 자식이 없는 A | bento:empty |
| 26 | `A:not(조건)`<br/>`apple:not(.small)`<br/>`apple:not(#big)` | 조건이 아닌 A | apple:not(.small) |
| 27 | `[B]` | \<?? B="anything"\> | [for] |
| 28 | `A[B]` | \<A B="anything"\> | plate[for] |
| 29 | `A[B="C"]` | \<A B="C"\>  | bento[for="Vitaly"] |
| 30 | `[A^="B"]` |  \<?? A="B로 시작하는 값"\> | [for^="Sa"] |
| 31 | `[A$="B"]` |  \<?? A="B로 끝나는 값"\> | [for$="to"] |
| 32 | `A[B*="C"]` | \<A B="C를 포함하는 값"\>  | bento[for*="obb"] |


**Success Notice:**  
수고하셨습니다. :+1:  
{: .notice--success}
 
