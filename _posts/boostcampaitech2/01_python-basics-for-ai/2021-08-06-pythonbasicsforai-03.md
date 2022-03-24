---
layout: post
title: "[Python Basics for AI] 3. 파이썬 기초 문법 2"
image: /assets/img/boostcampaitech2/cover.png
accent_image: 
  background: url('/assets/img/boostcampaitech2/cover.png') center/cover
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
description: >
  파이썬 기초 문법 2
categories:
  - boostcampaitech2
  - pythonbasicsforai
author: zgotter
sitemap: false
published: true
comments: true
---

# 3. [Python Basics for AI] 3. 파이썬 기초 문법 2

* 0.
{:toc}

## 3.1 Python Data Structure

### 3.1.1 `collections`

```python
from collections import deque
from collections import Counter
from collections import OrderedDict
from collections import defaultdict
from collections import namedtuple
```


#### 3.1.1.1 `deque`

- Stack 과 Queue 를 지원하는 모듈
- List에 비해 효율적인(=빠른 자료 저장 방식)을 지원함


```python
from collections import deque

deque_list = deque()
for i in range(5):
    deque_list.append(i) # append()
print(deque_list)
deque_list.appendleft(10) # appendleft()
print(deque_list)
```

    deque([0, 1, 2, 3, 4])
    deque([10, 0, 1, 2, 3, 4])



- rotate, reverse 등 Linked List의 특성을 지원
- 기존 list 형태의 함수를 모두 지원함


```python
deque_list.rotate(2) # 오른쪽으로 2칸 이동
print(deque_list)
deque_list.rotate(2) # 오른쪽으로 2칸 이동
print(deque_list)
```

    deque([3, 4, 10, 0, 1, 2])
    deque([1, 2, 3, 4, 10, 0])



```python
print(deque(reversed(deque_list)))
```

    deque([0, 10, 4, 3, 2, 1])



```python
deque_list.extend([5, 6, 7])
print(deque_list)

deque_list.extendleft([5, 6, 7])
print(deque_list)
```

    deque([1, 2, 3, 4, 10, 0, 5, 6, 7])
    deque([7, 6, 5, 1, 2, 3, 4, 10, 0, 5, 6, 7])



- deque는 기존 list 보다 효율적인 자료구조를 제공
- 효율적 메모리 구조로 처리 속도 향상


```python
# general list
import time

#start_time = time.clock()
start_time = time.time()
just_list = []
for i in range(10000):
    for i in range(10000):
        just_list.append(i)
        just_list.pop()

#print(time.clock() - start_time, 'seconds')
print(time.time() - start_time, 'seconds')
```

    25.48382806777954 seconds



```python
def general_list():
    just_list = []
    for i in range(100):
        for i in range(100):
            just_list.append(i)
            just_list.pop()

%timeit general_list()
```

    1000 loops, best of 5: 1.93 ms per loop



```python
# deque
from collections import deque
import time

start_time = time.time()
deque_list = deque()

# stack
for i in range(10000):
    for i in range(10000):
        deque_list.append(i)
        deque_list.pop()

print(time.time() - start_time, 'seconds')
```

    18.516666173934937 seconds



```python
from collections import deque

def deque_list():
    deque_list = deque()
    for i in range(100):
        for i in range(100):
            deque_list.append(i)
            deque_list.pop()    

%timeit deque_list()
```

    1000 loops, best of 5: 1.25 ms per loop



#### 3.1.1.2 OrderedDict

- dict와 달리, 데이터를 입력한 순서대로 dict을 반환함
- 그러나 dict도 python 3.6 부터 입력한 순서를 보장하여 출력함


#### 3.1.1.3 defaultdict

- dic type의 값에 기본 값을 지정
- 신규 값 생성 시 사용하는 방법


```python
d = dict()
print(d['first'])
```


    ---------------------------------------------------------------------------
    
    KeyError                                  Traceback (most recent call last)
    
    <ipython-input-11-05d3f1c0d1dc> in <module>()
          1 d = dict()
    ----> 2 print(d['first'])
    KeyError: 'first'



```python
from collections import defaultdict

d = defaultdict(object) # Default dictionary 를 생성
d = defaultdict(lambda: 0) # Default 값을 0으로 설정, 초기값은 함수 형태로 넣어줘야 한다.
print(d['first'])
```

    0



#### 3.1.1.4 Counter

- Sequence type의 data element 들의 갯수를 dict 형태로 반환


```python
from collections import Counter

c = Counter()
c = Counter('gallahad')
print(c)
```

    Counter({'a': 3, 'l': 2, 'g': 1, 'h': 1, 'd': 1})



```python
list(c.elements())
```


    ['g', 'a', 'a', 'a', 'l', 'l', 'h', 'd']

- set의 연산들을 지원함


#### 3.1.1.5 namedtuple

- tuple 형태로 Data 구조체를 저장하는 방법
- 저장되는 data의 variable을 사전에 지정해서 저장함


```python
from collections import namedtuple

Point = namedtuple('Point', ['x', 'y'])
p = Point(11, y=22)
print(p)
```

    Point(x=11, y=22)



```python
print(p[0] + p[1])
```

    33



```python
x, y = p
print(x, y)
```

    11 22



```python
print(p.x + p.y)
```

    33



```python
print(Point(x=11, y=22))
```

    Point(x=11, y=22)



## 3.2 Pythonic code

### 3.2.1 Contents

- split & join
- list comprehension
- enumerate & zip
- lambda & map & reduce
- iterable object
- generator
- asterisk (에스터리스크)


### 3.2.2 split & join


### 3.2.3 list comprehension


```python
import pprint

pprint.pprint('a')
```

    'a'



### 3.2.4 enumerate & zip

#### 3.2.4.1 enumerate


#### 3.2.4.2 zip

- 두 개의 list의 값을 병렬적으로 추출함


```python
alist = ['a1', 'a2', 'a3']
blist = ['b1', 'b2', 'b3']

for a, b in zip(alist, blist):
    print(a, b)
```

    a1 b1
    a2 b2
    a3 b3



```python
a, b, c = zip((1, 2, 3), (10, 20, 30), (100, 200, 300))
print(a, b, c)
```

    (1, 10, 100) (2, 20, 200) (3, 30, 300)



```python
[sum(x) for x in zip((1, 2, 3), (10, 20, 30), (100, 200, 300))]
```




    [111, 222, 333]




### 3.2.5 lambda & map & reduce

- 간단한 코드로 다양한 기능을 제공
- 그러나 코드의 직관성이 떨어져서 lambda 나 reduce는 python 3 에서 사용을 권장하지 않음
- Legacy library 나 다양한 머신러닝 코드에서 여전히 사용 중


#### 3.2.5.1 lambda

- 함수 이름 없이, 함수처럼 쓸 수 있는 익명 함수
- 수학의 람다 대수에서 유래함
- Python 3 부터는 권장하지는 않으나 여전히 많이 쓰임


```python
# general function

def f(x, y):
    return x + y

print(f(1, 4))
```

    5



```python
# lambda function
f = lambda x, y: x + y

print(f(1,4))
```

    5



```python
# lambda function
(lambda x, y: x + y)(1, 4)
```




    5




#### 3.2.5.2 map

- sequence data 에 함수를 mapping
  - `map(함수, sequence 데이터)`
- 두 개 이상의 list에도 적용 가능함
  - `map(함수, sequence 데이터 1, sequence 데이터 2)`
- if filter 도 사용 가능
  - `map(if filter 가 적용된 함수, sequence 데이터)`
- map 함수의 수행 결과는 generator 가 리턴되기 때문에 `list()` 를 이용하여 형변환해줘야 한다.
  - python 3 는 iteration을 생성
  - list를 붙여줘야 list 사용 가능
- 최근에는 map 함수 사용을 권장하지 않음 (list comprehension 으로 대체 가능)


```python
ex = [1, 2, 3, 4, 5]
f = lambda x: x ** 2

list(map(f, ex))
```




    [1, 4, 9, 16, 25]




```python
ex = [1, 2, 3, 4, 5]
f = lambda x, y: x + y
print(list(map(f, ex, ex)))
```

    [2, 4, 6, 8, 10]



#### 3.2.5.3 reduce

- map function 과 달리 list에 똑같은 함수를 적용해서 통합
- 대용량 데이터 처리 시 사용
- 요즘에는 많이 사용하지 않음


```python
from functools import reduce

print(reduce(lambda x, y: x + y, [1, 2, 3, 4, 5]))
# 1+2=3
# 3+3=6
# 6+4=10
# 10+5=15
```

    15



### 3.2.6 iterable object

- sequence 형 자료형에서 데이터를 순서대로 추출하는 object
- 내부적 구현으로 `__iter__` 와 `__next__` 가 사용됨
- `iter()` 와 `next()` 함수로 iterable 객체를 iterator object 로 사용
- 특정 데이터에서 다음 데이터의 메모리 주소값을 저장하고 있는다.


```python
cities = ['Seoul', 'Busan', 'Jeju']

iter_obj = iter(cities) # memory address 를 가져온다.
print(iter_obj)
print()

print(next(iter_obj)) # next() 함수를 사용해 실제 값을 가져온다.
print(next(iter_obj))
print(next(iter_obj))
next(iter_obj) # 더 이상 데이터가 없을 경우 'StopIteration' 에러 발생
```

    <list_iterator object at 0x7f8a95cc9390>
    
    Seoul
    Busan
    Jeju



    ---------------------------------------------------------------------------
    
    StopIteration                             Traceback (most recent call last)
    
    <ipython-input-37-fe42bb129912> in <module>()
          8 print(next(iter_obj))
          9 print(next(iter_obj))
    ---> 10 next(iter_obj)
    StopIteration: 



### 3.2.7 generator


#### 3.2.7.1 generator 란

- iterable object를 특수한 형태로 사용해주는 함수
- element 가 사용되는 시점에 값을 메모리에 반환 (그 전에는 주소값만 가지고 있음)
- `yield` 를 사용해 한 번에 하나의 element만 반환함
- 메모리를 절약할 수 있음


```python
# 일반적인 경우
def general_list(value):
    result = []
    for i in range(value):
        result.append(i)
    return result

print(general_list(50))
```

    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49]



```python
import sys
result = general_list(50)
sys.getsizeof(result)
```




    536




```python
# generator
def generator_list(value):
    result = []
    for i in range(value):
        yield i # 값을 메모리에 올리지 않고, 메모리의 주소값만 가지고 있음. 호출할 때 데이터를 출력

print(generator_list(50)) # generator 객체가 생성됨
```

    <generator object generator_list at 0x7f8a95c9fc50>



```python
# 해당 generator 를 호출할 때 값을 return 한다.
for a in generator_list(50):
    print(a)
```

    0
    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13
    14
    15
    16
    17
    18
    19
    20
    21
    22
    23
    24
    25
    26
    27
    28
    29
    30
    31
    32
    33
    34
    35
    36
    37
    38
    39
    40
    41
    42
    43
    44
    45
    46
    47
    48
    49



```python
import sys
result = generator_list(50)
sys.getsizeof(result)
```




    128




#### 3.2.7.2 generator comprehension

- list comprehension과 유사한 형태로 generator 형태의 list 생성
- generator expression 이라는 이름으로도 부름
- `[]` 대신 `()` 를 사용하여 표현


```python
gen_ex = (n*n for n in range(50))
print(gen_ex)
print(type(gen_ex))
```

    <generator object <genexpr> at 0x7f8a95c54f50>
    <class 'generator'>



```python
# generator 사용
print(list(gen_ex))
```

    [0, 1, 4, 9, 16, 25, 36, 49, 64, 81, 100, 121, 144, 169, 196, 225, 256, 289, 324, 361, 400, 441, 484, 529, 576, 625, 676, 729, 784, 841, 900, 961, 1024, 1089, 1156, 1225, 1296, 1369, 1444, 1521, 1600, 1681, 1764, 1849, 1936, 2025, 2116, 2209, 2304, 2401]



#### 3.2.7.3 메모리 효율성

- 일반적인 iterator 는 generator 에 반해 훨씬 큰 메모리 용량 사용


```python
from sys import getsizeof

gen_ex = (n*n for n in range(500))
print(getsizeof(gen_ex))
print(getsizeof(list(gen_ex)))

list_ex = [n*n for n in range(500)]
print(getsizeof(list_ex))
```

    128
    4584
    4280



#### 3.2.7.4 When generator

- list 타입의 데이터를 반환해주는 함수는 generator 로 만들어라
  - 읽기 쉬운 장점
  - 중간 과정에서 loop 이 중단될 수 있을 때
- 큰 데이터를 처리할 때는 generator expression 을 고려하라
  - 데이터가 커도 처리의 어려움이 없음
- 파일 데이터를 처리할 때도 generator를 쓰자


### 3.2.8 function passing arguments

- 함수에 입력되는 arguments 의 다양한 형태
  - Keyword arguments
  - Default arguments
  - Variable-length(가변) arguments


#### 3.2.8.1 Keyword arguments

- 함수에 입력되는 parameter의 **변수명을 사용**하여 arguments를 넘김


```python
def print_something(my_name, your_name):
    print(f"Hello {your_name}, My name is {my_name}")

print_something('Sunghan', 'TEAMLAB')
print_something(your_name='TEAMLAB', my_name='Sunghan')
```

    Hello TEAMLAB, My name is Sunghan
    Hello TEAMLAB, My name is Sunghan



#### 3.2.8.2 Default arguments

- parameter의 기본값을 사용
- 입력하지 않을 경우 기본값 출력


```python
def print_something_2(my_name, your_name='TEAMLAB'):
    print(f"Hello {your_name}, My name is {my_name}")

print_something_2('Sunghan', 'TEAMLAB')
print_something_2('Sunghan')
```

    Hello TEAMLAB, My name is Sunghan
    Hello TEAMLAB, My name is Sunghan



#### 3.2.8.3 Variable-length with asterisk

- 가변길이 에스터리스크
- 함수의 parameter가 정해지지 않은 경우 사용
  - ex) 다항 방정식, 마트 물건 계산 함수


##### 3.2.8.3.1 가변 인자 (variable-length)

- 개수가 정해지지 않은 변수를 함수의 parameter로 사용하는 법
- Keyword arguments와 함께, argument 추가가 가능
- **Asterisk(`*`)** 기호를 사용하여 함수의 parameter를 표시함
- 입력된 값은 **tuple type**으로 사용할 수 있음
- 가변인자는 오직 한 개만 맨 마지막 parameter 위치에 사용 가능

- 가변 인자는 일반적으로 `*args` 를 변수명으로 사용
- 기존 parameter 이후에 나오는 값을 tuple로 저장함


```python
def asterisk_test(a, b, *args):
    print(args)
    print(type(args))
    return a + b + sum(args)

print(asterisk_test(1, 2, 3, 4, 5))
```

    (3, 4, 5)
    <class 'tuple'>
    15



##### 3.2.8.3.2 키워드 가변 인자 (Keyword variable-length)

- parameter 이름을 따로 지정하지 않고 입력하는 방법
- **asterisk(`*`) 두 개를 사용**하여 함수의 parameter 를 표시함
- 입력된 값은 **dict type**으로 사용할 수 있음
- 가변 인자는 오직 한 개만 기존 가변 인자 다음에 사용


```python
def kwargs_test_1(**kwargs):
    print(kwargs)
    print(type(kwargs))

kwargs_test_1(first=3, second=4, third=5)
```

    {'first': 3, 'second': 4, 'third': 5}
    <class 'dict'>



```python
def kwargs_test_3(one, two=3, *args, **kwargs):
    print(one+two+sum(args))
    print(args)
    print(kwargs)

# 키워드 없이 사용하고, 뒤에 키워드를 사용하는 것은 가능하다. (키워드 x -> 키워드 o : 가능)
kwargs_test_3(10, 30, 3, 4, 5, 6, 7, 8, first=3, second=4, third=5)
```

    73
    (3, 4, 5, 6, 7, 8)
    {'first': 3, 'second': 4, 'third': 5}



```python
# 키워드를 사용하면 중간에 키워드 없이 사용이 불가능하다. (키워드 o -> 키워드 x : 불가능)
kwargs_test_3(one=10, two=30, 3, 4, 5, 6, 7, 8, first=3, second=4, third=5)
```


      File "<ipython-input-66-e8fc07aea9c0>", line 2
        kwargs_test_3(one=10, two=30, 3, 4, 5, 6, 7, 8, first=3, second=4, third=5)
                                     ^
    SyntaxError: positional argument follows keyword argument




```python
kwargs_test_3(one=10, two=30, first=3, second=4, third=5)
```

    40
    ()
    {'first': 3, 'second': 4, 'third': 5}



##### 3.2.8.3.3 asterisk (`*`)

- 흔히 알고 있는 `*` 를 의미함
- 단순 곱셈, 제곱 연산, 가변 인자 활용 등 다양하게 사용됨

- asterisk 를 이용하여 tuple, dict 등 자료형에 들어가 있는 값을 **unpacking** 할 수 있다.
- 함수의 입력값, zip 등에 유용하게 사용 가능


```python
def asterisk_test(a, *args):
    print(a, args)
    print(type(args))

asterisk_test(1, *(2,3,4,5,6)) # unpacking
```

    1 (2, 3, 4, 5, 6)
    <class 'tuple'>



```python
def asterisk_test(a, *args):
    print(a, args)
    print(type(args)) # args : 튜플 안에 튜플이 들어감

asterisk_test(1, (2,3,4,5,6))
```

    1 ((2, 3, 4, 5, 6),)
    <class 'tuple'>



```python
print('a', 'b', 'c', 'd')
```

    a b c d



```python
print(['a', 'b', 'c', 'd'])
```

    ['a', 'b', 'c', 'd']



```python
print(*['a', 'b', 'c', 'd']) # list unpacking 
```

    a b c d



```python
a, b, c = ([1, 2], [3, 4], [5, 6])
print(a, b, c)
```

    [1, 2] [3, 4] [5, 6]



```python
data = ([1, 2], [3, 4], [5, 6])
print(*data)
```

    [1, 2] [3, 4] [5, 6]



```python
def asterisk_test(a, b, c, d):
    print(a, b, c, d)

data = {'b': 1, 'c': 2, 'd': 3}
asterisk_test(10, **data) # dictionary 는 키워드 가변인자 식으로 unpacking
```

    10 1 2 3



```python
# with zip (1)
ex = ([1, 2], [3, 4], [5, 6], [5, 6], [5, 6])
for value in zip(ex):
    print(value)
```

    ([1, 2],)
    ([3, 4],)
    ([5, 6],)
    ([5, 6],)
    ([5, 6],)



```python
# with zip (2)
ex = ([1, 2], [3, 4], [5, 6], [5, 6], [5, 6])
for value in zip(*ex): # unpacking
    print(value)
```

    (1, 3, 5, 5, 5)
    (2, 4, 6, 6, 6)



```python
for data in zip(*([1, 2], [3, 4], [5, 6])):
    print(data)
```

    (1, 3, 5)
    (2, 4, 6)

