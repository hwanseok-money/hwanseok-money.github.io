---
title: "[Python] 쉽게 정리한 파이썬이 동작하는 원리"
excerpt: "build, compile, link, RPython, CPython 그리고 PyPy"
date: 2021-01-28
last_modified_at:
categories:
  - Python
tags:
  - Python
  - IO
  - FastIO
  - build
  - compiler
  - link
  - Cpython
  - Rpython
  - pypy
  - interpreter
  - binary code
  - byte code
  - object file
  - executable
  - RPython translation toolchain
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

# Build, Compile, Link

**Build = Compile + Link**  

Build의 가장 기본적인 의미는 프로그래밍 언어를 기계어로 바꾸어주는 과정입니다. 먼저 C나 java 같은 native code에서 *.o파일(오브젝트 파일)을 만드는 것을 컴파일이라고 합니다. 이는 개발자가 작성한 소스코드를 binary code로 변환하는 과정을 의미합니다. 그리고 *.o파일에서 .exe파일을 만드는 것을 Link라고 합니다. 기능별로 분할된 여러 개의 native code들이 있을 때 각각을 *.o파일로 컴파일 하고, 다수의 *.o파일을 하나의 *.exe파일을 만드는 것을 Link라고 하는 것입니다. 링크라고 부르는 것은 하나의 파일에서 다른 파일의 코드를 사용해야하는데 이를 가능하도록 연결해주기 때문이라고 기억하면 됩니다. 컴파일과 링크를 합쳐서 실행가능한 파일을 만드는 과정을 빌드라고 부릅니다.  

- native code란? : OS에 의해서 직접적으로 컴파일 되는 코드를 의미합니다. 예를 들어서 C/C++ 입니다.
- managed code란? : 구동을 시키기 위해서 interpreter라고 불리는 다른 프로그램이 반드시 요구되는 코드를 의미합니다. 예를 들어서 C#, java, python입니다.
- 네이비브와 메니지드를 굳이 명확해서 구분해서 사용하는 것 같지는 않습니다.

# Binary Code, Byte Code  

C언어를 기반으로한 소스코드.c를 컴파일하면 오브젝트.o 파일이 생성됩니다. 오브젝트 파일은 0과 1로 이루어져 있습니다. 즉, 컴파일 후에 이미 컴퓨터가 이해할 수 있는 이진 코드로 변환된 상태입니다. 오브젝트 파일은 컴퓨터가 이해할 수 있는 구조이지만 실행할 수는 없는 형태입니다. 완전히 기계어로 변환되어야(Link)되어야 실행될 수 있기 때문입니다. 반대로 생각하면 실행파일은 컴퓨터가 이해할 수 있는 완벽한 기계어입니다.  

Java에서는 컴파일러Javac에 의해서 소스파일.java가 오브젝트.class로 변환될 때 0과 1로 이루어진 바이너리 이진코드가 되는 것이 아니라, byte code로 변환됩니다. Byte Code는 가상 머신이 이해할 수 있는 언어입니다. 즉, java의 가상 머신에서 이해할 수 있는 정도로 컴파일된다고 생각하면 됩니다. Byte Code는 다시 실시간 번역기 Just-In-Time(JIT) Compiler에 의해서 실시간으로 기계어를 생성합니다. 

# Python

두 가지 의미가 있습니다.
1. 프로그래밍 언어
1. 파이썬 언어를 이해하고 실행하는 구현체(Implementation)

CPython과 PyPy는 모두 Python 구현체입니다. 여기서 `구현체`라는 말을 우선은 interpreter라고 생각하고, 아래 내용을 읽으면서 하나씩 제대로 이해하는게 좋습니다.  

## Cpython

CPython is the reference implementation of the Python programming language. Written in C and Python, CPython is the default and most widely used implementation of the language. **CPython can be defined as both an interpreter and a compiler as it compiles Python code into bytecode before interpreting it.**  

CPython은 Python Code를 bytecode로 컴파일 한 뒤, interpreting하기 때문에 commpiler이자 interpreter입니다.  


## RPython

RPython은 그 자체로 언어가 아닙니다. Python Language의 부분집합입니다. RPython에 대한 정의는, 어떤 syntax가 아니라, `RPython translation toolchain`이라는 framework가 accept할 수 있는 모든 것입니다.  

모든 RPython 코드는 Python interpreter로 실행될 수 있습니다. 차이점은 RPython을 `RPython translation toolchain`을 사용해서 `컴파일`하면 C code기반의 바이너리가 생성됩니다. 따라서 컴파일 이후에는 더 빠르게 실행할 수 있다는 장점이 있습니다. 하지만 아직 모든 python의 feature를 지원하지는 못한다는 단점이 있습니다.  

## Pypy

pypy라고 하면 두 가지의미가 있습니다. 첫 번째는 `RPython translation toolchain`를 의미합니다. 두 번째는 `RPython translation toolchain`과 함께 생성된 파이썬의 특정 구현을 의미합니다. 하지만 일반적으로 pypy는 두 번째를 의미하며 `RPython translation toolchain`는 `RPython translation toolchain`라고 명시적으로 언급합니다.  

1. RPython으로 소스코드를 작성하고
1. `RPython translation toolchain`을 적용하여 c 기반 binary를 생성하고
1. 이 binary를 실행하기 위해서 python interperter인 PyPy를 사용합니다.   

- `PyPy` = `the Python implementation` = `Python interpreter produced with RPython translation toolchain`
- `RPython translation toolchain` = `framework`.

# 정리

- Python Code ---CPython---> Byte Code로 변환 ---CPython---> interpreting -> 실행
- RPython Code ---RPython translation toolchain--> C 기반 Binary Code로 변환한 뒤 ---PyPy--> 실행 

# Reference

- <https://shrtorznzl.tistory.com/82>
- <https://maori.geek.nz/rpython-is-not-a-language-an-introduction-to-the-rpython-language-9f48c7a3047>
- <https://doc.pypy.org/en/latest/introduction.html>  

**Success Notice:**
수고하셨습니다. :+1:
{: .notice--success}