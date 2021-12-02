---
layout: post
title: "[Python Basics for AI] 2. 파이썬 기초 문법"
description: >
  파이썬 기초 문법
categories:
  - post
  - boostcampaitech2
  - pythonbasicsforai
author: zgotter
sitemap: false
published: true
---

# 2. [Python Basics for AI] 2. 파이썬 기초 문법

* toc
  {:toc}

## 2.1 변수 (Variables)

생략

## 2.2 함수와 콘솔 I/O (Function and Console I/O)

### 2.2.1 함수


```python
def f(x):
    return 2*x + 7

def g(x):
    return x**2

x = 2
print(f(x) + g(x) + f(g(x)) + g(f(x))) # 151
```

    151


<br>

## 2.3 Conditionals and Loops

생략

## 2.4 String and advanced function concept

### 2.4.1 function type hints

- 파이썬의 가장 큰 특징 : dynamic typing
  - 처음 함수를 사용하는 사용자가 interface를 알기 어렵다는 단점이 있음
- python 3.5 버전 이후로는 PEP 484 에 기반하여 type hints 기능 제공

```python
def do_function(var_name: var_type) -> return_type:
    pass
```


```python
def type_hint_example(name: str) -> str: # (파라미터명: 타입) -> 리턴 타입
    return f"Hello, {name}"
```


```python
type_hint_example('sunghan')
```




    'Hello, sunghan'



<br>

**Type hints의 장점**

- 사용자에게 인터페이스를 명확히 알려줄 수 있다.
- 함수의 문서화 시 parameter에 대한 정보를 명확히 알 수 있다.
- mypy 또는 IDE, linter 등을 통해 코드의 발생 가능한 오류를 사전에 확인
- 시스템 전체적인 안정성을 확보할 수 있다.


<br>

### 2.4.2 function docstring

- 파이썬 함수에 대한 상세스펙을 사전에 작성 (함수 사용자의 이해도 up)
- 세개의 따옴표로 docstring 영역 표시 (함수명 아래)

```python
def kos_root():
    """Return the pathname of the KOS root directory."""
    global _kos_root
    if _kos_root: return _kos_root
```


```python
def add_binary(a, b):
    """
    Returns the sum of two decimal numbers in binary digits.

        Parameters:
            a (int): A decimal integer
            b (int): Another decimal integer

        Returns:
            binary_sum (str): Binary string of the sum of a and b

        Examples:
            a = 10, b = 15
            binary_sum = "11001"

    """
    binary_sum = bin(a+b)[2:]
    return binary_sum

print(add_binary(10, 15))
```

    11001


<br>

- vscode 의 `Python Docstring Generator` extensions 를 설치하면 손쉽게 docstring 을 작성할 수 있다.
  - `Ctrl + Shift + P` -> `Generate Docstring`

<br>

### 2.4.3 함수 작성 가이드 라인

- 가능하면 짧게 작성
- 함수명은 소문자로 구성, 필요하면 밑줄로 나눔
- 함수 이름에 함수의 역할, 의도가 명확히 들어낼 것
  - v, o : ~를 한다.
  - 띄어쓰기는 `_` 사용
  - ex) `print_hello_world()`
- 하나의 함수에는 유사한 역할을 하는 코드만 포함
- 인자로 받은 값 자체를 바꾸진 말 것 (임시 변수 선언)
