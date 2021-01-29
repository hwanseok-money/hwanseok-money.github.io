---
title: "[Python] 다양한 정렬 방법"
excerpt: ""
date: 2021-01-28
last_modified_at: 
categories:
  - Python
tags:
  - Python
  - IO
  - FastIO
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

# 객체와 이름은 별도의 것이다

# 변수는 상자가 아니다

파이썬 변수는 자바에서의 참조 변수와 같습니다. 객체에 붙은 레이블이라고 생각하면 좋습니다.  

```python
>>> a = [1,2,3]
>>> b = a
>>> a.append(4)
>>> b
[1, 2, 3, 4]
>>> 
```

객체는 변수가 할당되기 전에 생성됩니다. `객체를 (만들어서) 변수에 할당했다`보다는 `변수가 (이미 존재하는) 객체에 할당되었다`고 표현하는 것이 더 타당합니다.  

아래의 예시에서보면 y에 할당하는 라인에서 에러가 발생했다는 것을 알 수 있습니다. dir()은 어떤 객체를 인자로 전달하면 해당 객체가 어떤 변수와 메서드를 가지고 있는지 나열해주는 기능을 가지고 있습니다. 아래의 예시를 보면 y변수는 생성되지 않았습니다.  

```python
>>> class Gizmo:
...     def __init__(self):
...         print('Gizmo id: %d' % id(self))
... 
>>> x = Gizmo()
Gizmo id: 140250071990528 # 첫 번째 Gizmo 객체가 생성되었다. 
>>> y = Gizmo() * 10
Gizmo id: 140250080940384 # 두 번째 Gizmo 객체가 생성되었다.
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unsupported operand type(s) for *: 'Gizmo' and 'int'
>>> dir()
['Gizmo', '__annotations__', '__builtins__', '__doc__', '__loader__', '__name__', '__package__', '__spec__', 'x']
```

다시 강조하면, 객체를 성공적으로 생성한 뒤에 변수이름을 가진 라벨을 붙히는 것이라고 생각하는 것이 옳은 방향입니다. 그래서 변수에 여러 이름을 붙히는 것도 가능합니다. 

# 객체의 정체성, 동질성, 별명

객체 x의 정체성은 id(x)로 확인할 수 있습니다. 두 dict내의 요소가 동일하다고 해도 두 dict의 id를 다를 수 밖에 없습니다. `__eq__()`에 의해서 두 dict가 동일하다고 판단되어도 두 dict가 IS 관계에서는 False입니다.  

모든 객체는 정체성, 자료형, 값을 가지고 있습니다. 객체의 정체성은 일단 생성한 후에는 결코 변하지 않습니다. 정체성은 메모리 내의 객체 주소라고 생각할 수 있습니다. IS 연산자는 두 객체의 정체성을 비교합니다. id()는 정체성을 나타내는 정수를 반환합니다.  

CPython에서는 id()가 객체의 메모리를 반환하지만 다른 파이썬 인터프리터에서는 메모리 주소 이외의 값을 반환할 수 있습니다. 그럼에도 ID는 객체의 고유한 레이블이라는 것을 보장할 수 있습니다.  

일반적인 경우 IS보다 ==를 더 많이 사용합니다. IS는 싱글톤과 비교할 때 None과 비교하는 경우가 일반적입니다.  

```python
x is None
```

# 튜플의 참조 형태

리스트, 딕셔너리, 집합 등 대부분의 파이썬 컬렉션 그리고 튜플은 객체에 대한 참조를 담습니다. 예외적으로 데이터를 물리적으로 연속된 메모리에 저장하는 것은 `str, bytes, array.array`와 같은 단일형 시퀀스뿐입니다.  

튜플을 제대로 알지 못하면 튜플은 불변하다고 알게됩니다. 튜플은 어떤 항목을 참조하는지에 대한 정보가 불변하고, 참조되는 항목은 변할 수 있습니다.  

```python
t1 = (1, 2, [30, 40])
t2 = (1, 2, [30, 40])
print(t1 == t2)  # True
print(id(t1[-1]))  # 140576015904192
t1[-1].append(99)
print(id(t1[-1]))  # 140576015904192
print(t1 == t2)  # False
```  

t1은 불변형이지만, t1[-1]은 list이므로 가변형입니다. t1[-1]의 값을 바꾸어도 t1이 가진 t1[-1]의 정체성을 불변합니다. 하지만 ==의 구현에 의해서 참조되는 값을 비교하게 되고 마지막에는 False를 리턴합니다.  

# 얕은 복사, 깊은 복사 

위의 예시와 같이 객체가 다른 객체를 담고 있을 때는 객체를 복사할 때는 어떻게 해야할까요? 내부 객체를 복사해도 되고, 내부 객체를 공유해도 됩니다. 정답은 없습니다!  

얕게 복사하는 것은 내포된 객체의 참조를 공유하도록 복사하는 것을 말합니다. 깊게 복사하는 것은 내포된 객체의 참조를 공유하지 않도록 복사하는 것을 말합니다.    

리스트나 대부분의 내장 가변 컬렉션을 복사하는 가장 손쉬운 방법은 그 자료형 객체의 내장 생성자를 사용하는 것입니다. `b = list(a)`또는 `b = a[:]`는 얕은 복사입니다. ==를 사용할 때는 True이겠지만, IS 관계에서 두 객체의 정체성은 다릅니다. 이 때, 최상위 컨테이너는 복제하지만, 사본은 원래 컨테이너에 들어 있던 동일 객체에 대한 참조로 채워집니다. 모든 항목이 불변형이면 이 방식은 메모리를 절약합니다.(값을 복사해서 새로운 메모리를  사용하지 않습니다.) 내부에 포함된 객체에 대한 참조값만 복사하면 됩니다. 하지만 가변형이 포함되어 있는 객체를 복사하는 경우 문제가 발생할 수 있습니다. (복사한 값에서 참조하고 있는 값을 수정했을 때, 원본이 함께 참조하고 있어서 값의 변경이 동일하게 적용될 수 있습니다.) 

```python
a = [1, [2], (3,)]
# 얕은 복사
## 1 : 가장 외부 컨테이너에 포함된 1은 값이 복사가 된다.
## 2 : [2]는 별도의 메모리에 저장되어있고 a에서 이를 참조하고 있었다. b도 같은 메모리를 참조한다.
## 3 : (3,)도 별도의 메모리에 저장되어 있었고 a와 b가 모두 같은 메모리를 참조한다.
b = list(a)
# a만 참조하는 메모리에 추가된다.
a.append(100)
# a와 b가 모두 참조하고 있는 메모리에서 삭제된다.
a[1].remove(2)
print('a:', a)
print('b:', b)
# b[1]는 가별 시퀀스이기 때문에 a와 b가 모두 참조하고 있는 메모리에서 삭제된다.
b[1] += [2,22]
# b[2]는 불변 시퀀스이기 때문에 새로운 튜플이 생성되고 이 메모리를 b만 참조하게 된다.
b[2] += (33,333)
print('a:', a)
print('b:', b)
```  

얕은 복사는 import copy 이후 copy()를 사용하고, 깊은 복사는 from copy import deepcopy 이후 deepcopy()를 사용합니다. 사용 예시는 docs를 참조합니다.  

# 참조로서의 함수 매개변수

파이썬은 함수 호출에서 Call by sharing의 매개변수 전달 방식만을 지원합니다. 공유로 호출한다는 말은 함수의 각 매개변수가 인수로 전달받은 각 참조의 사본을 받는다는 의미입니다. 즉, 함수 안의 매개변수는 실제 인수의 별명이 됩니다. 함수 안에서 값을 바꾸면, 자료형에 따라서 밖에서도 변화가 생길 수 있습니다.   

```python
x = 1
y = 2
print(add(x, y)) # 1 2
print(x, y)  # 1,2 변하지지 않음
t = (10, 20)
u = (30, 40)
print(add(t, u)) # (10, 20, 30, 40)
print(t, u)  # (10,20),(30,40) 변하지지 않음
a = [1, 2]
b = [3, 4]
print(add(a, b)) # [1, 2, 3, 4]
print(a, b)  # [1,2,3,4], [3,4]로 변함!!
```

## 가변 매개변수가 기본이 될 때의 문제점

가변 매개변수인 []를 기본값으로 지정하면, 아래와 같이 기본 매개변수를 공유하게되는 문제가 발생합니다.  

```python
class Bus:
    def __init__(self, passengers=[]):
        self.passengers = passengers

    def pick(self, name):
        self.passengers.append(name)

    def drop(self, name):
        self.passengers.remove(name)


bus1 = Bus(['A', 'B'])
print(bus1.passengers)  # ['A', 'B']
bus1.pick('C')
bus1.drop('B')
print(bus1.passengers)  # ['A', 'C']

bus2 = Bus()
bus2.pick('1')
print(bus2.passengers)  # ['1']
bus3 = Bus()
print(bus3.passengers)  # ['1'] bus2과 passengers를 공유!
bus3.drop('1')
print(bus2.passengers)  # [] bus3과 passengers를 공유!
print(bus3.passengers)  # [] bus2과 passengers를 공유!
print(bus2.passengers is bus3.passengers) #True
```  

일반적으로 모듈이 로딩될 때, 속성의 기본값이 평가되고 함수 객체의 속성이 됩니다. 따라서 self.passengers = passengers를 통해서 동일한 함수 객체에 대한 라벨이 추가되는 문제입니다.  

## 함수 호출자가 전달한 가변 인수의 안전한 처리

위의 문제를 막기 위해서는 다음과 같이 해야합니다.  

```python
class Bus:
    def __init__(self, passengers=None):
        if passengers is None:
            self.passengers = []
        else :
            # 전달받은 passengers의 값을 변경할 위험성!
            # self.passengers = passengers
            # list 생성사로 얕은 복사만을 해도 되는 경우
            self.passengers = list(passengers)

    def pick(self, name):
        self.passengers.append(name)

    def drop(self, name):
        self.passengers.remove(name)
```
 
`self.passengers = list(passengers)`에서 깊은 복사를 사용해야하는 경우는 깊은 복사를 사용해야 합니다.  

# del 명령 및 가비지 컬렉션

del 명령은 이름을 제거하는 것이지, 객체를 제거하는 것이 아닙니다. del명령의 결과로 가비지 컬렉트될 수 있지만, 제거된 변수가 객체를 참조하는 최후의 변수거나 객체에 도달할 수 없을 때에만 가비지 컬렉트됩니다.  

`__del__()` 메서드는 객체가 제거되기 직전에 외부 리소스를 해제할 기회를 제공하기 위해서 존재합니다. 직접 객체를 제거하는 역할을 수행하지 않습니다.  

CPython의 경우 가비지 컬렉션은 주로 `참조 카운트`에 기반합니다. 본질적으로 각 객체는 얼마나 많은 참조가 자신을 가리키는지 개수를 세고 있습니다. refcount가 0이 되자마자 Cpython이  객체의 `__def__()`를 호출하고 객체에 할당되어 있는 메모미를 해제함으로써 객체가 제거됩니다.  

CPython2.0에는 순환참조(서로를 참조하고 있어 refcount는 0이 아니지만 도달할 수 없는 상태)에 관련된 객체 그룹을 탐색하기 위해 세대별 가비지 컬렉션 알고리즘을 추가했습니다.  

다른 파이썬 구현에서는 더 정교한 가비지 컬렉터를 사용하므로, 객체에 대한 참조가 모두 사라진 경우에도 `__del__()`메서드가 바로 호출되지 않을 수도 있습니다.  

# 약한 참조 : 객체를 보존하지 않으면서 객체를 기억하기 위한 방법

weakref.finalize는 객체가 소멸될 때 수행되는 콜백을 등록하는 기능을 가집니다.  

```python
import weakref


def bye():
    print('Good Bye')


s1 = {1, 2, 3}
s2 = s1
ender = weakref.finalize(s1, bye)
print(ender.alive) # True
del s1
print(ender.alive) # True
s2 = 'New Friend' # Good Bye
print(ender.alive) # False
```  

객체가 메모리에 유지되거나 유지되지 않도록 만드는 것은 참조의 존재 여부입니다. 


# Reference

- Fluent Python 8장

**Success Notice:**
수고하셨습니다. :+1:
{: .notice--success}