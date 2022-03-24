---
layout: post
title: "[Python Basics for AI] 6. Exception / File / Log Handling"
image: /assets/img/boostcampaitech2/cover.png
accent_image: 
  background: url('/assets/img/boostcampaitech2/cover.png') center/cover
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
description: >
  Exception / File / Log Handling
categories:
  - boostcampaitech2
  - pythonbasicsforai
author: zgotter
sitemap: false
published: true
comments: true
---

# 6. [Python Basics for AI] 6. Exception / File / Log Handling

* 0.
{:toc}

## 6.1 Exception Handling

### 6.1.1 Exception

- 예상 가능한 예외
- 예상이 불가능한 예외


### 6.1.2 예상 가능한 예외

- 발생 여부를 사전에 인지할 수 있는 예외
- ex) 사용자의 잘못된 입력, 파일 호출 시 파일 없음
- 개발자가 반드시 명시적으로 정의 해야 함


### 6.1.3 예상 불가능한 예외

- 인터프리터 과정에서 발생하는 예외 (개발자 실수)
- ex) 리스트의 범위를 넘어가는 값 호출, 정수 0으로 나눔
- 수행 불가 시 인터프리터가 자동 호출


### 6.1.4 예외 처리 (Exception Handling)

- 예외가 발생할 경우 후속 조치 등 대처 필요


### 6.1.5 파이썬의 예외 처리

#### 6.1.5.1 `try ~ except` 문법

```python
try:
    예외 발생 가능 코드
except <Exception Type>:
    예외 발생 시 대응하는 코드
```


```python
for i in range(10):
    try:
        print(i, 10//i)
    except ZeroDivisionError: # ZeroDivisionError : built-in error
        print('Not divided by 0')
```

    Not divided by 0
    1 10
    2 5
    3 3
    4 2
    5 2
    6 1
    7 1
    8 1
    9 1



#### 6.1.5.2 exception 의 종류

- built-in exception : 기본적으로 제공하는 예외
  - `IndexError` : List의 Index 범위를 넘어갈 때
  - `NameError` : 존재하지 않은 변수를 호출할 때
  - `ZeroDivisionError` : 0으로 숫자를 나눌 때
  - `ValueError` : 변환할 수 없는 문자/숫자를 변환할 때
  - `FileNotFoundError` : 존재하지 않는 파일을 호출할 때


```python
a = [1, 2, 3, 4, 5]
for i in range(10):
    try:
        print(i, 10//i)
        print('a : ', a[i])
        print(v)
    except ZeroDivisionError: # ZeroDivisionError : built-in error
        print('Not divided by 0')
    except IndexError as e:
        print(e)
    except Exception as e: # 모든 예외를 다 처리할 수 있음 (권장하지 않음)
        print(e)
```

    Not divided by 0
    1 10
    a :  2
    name 'v' is not defined
    2 5
    a :  3
    name 'v' is not defined
    3 3
    a :  4
    name 'v' is not defined
    4 2
    a :  5
    name 'v' is not defined
    5 2
    list index out of range
    6 1
    list index out of range
    7 1
    list index out of range
    8 1
    list index out of range
    9 1
    list index out of range



#### 6.1.5.3 `try ~ except ~ else`

```python
try:
    예외 발생 가능 코드
except <Exception Type>:
    예외 발생 시 동작하는 코드
else:
    예외가 발생하지 않을 때 동작하는 코드
```

- 해당구조는 이해하기 때문에 사용을 권장하지 않는다.


#### 6.1.5.4 `try ~ except ~ finally`

```python
try:
    예외 발생 가능 코드
except <Exception Type>:
    예외 발생 시 동작하는 코드
finally:
    예외 발생 여부와 상관없이 실행됨
```


#### 6.1.5.5 `raise` 구문

- 필요에 따라 강제로 Exception을 발생

```python
raise <Exception Type>(예외 정보)
```


```python
while True:
    value = input('변환할 정수 값을 입력하세요 : ')
    for digit in value:
        if digit not in '0123456789':
            raise ValueError('숫자값을 입력하지 않으셨습니다.')
    print('정수값으로 변환된 숫자 -', int(value))
```

    변환할 정수 값을 입력하세요 : 5
    정수값으로 변환된 숫자 - 5
    변환할 정수 값을 입력하세요 : d



    ---------------------------------------------------------------------------
    
    ValueError                                Traceback (most recent call last)
    
    <ipython-input-7-be8fdac4c6b3> in <module>()
          3     for digit in value:
          4         if digit not in '0123456789':
    ----> 5             raise ValueError('숫자값을 입력하지 않으셨습니다.')
          6     print('정수값으로 변환된 숫자 -', int(value))
          
    ValueError: 숫자값을 입력하지 않으셨습니다.



#### 6.1.5.6 `assert` 구문

- 특정 조건에 만족하지 않을 경우 예외 발생

```python
assert 예외조건
```


```python
def get_binary_number(decimal_number: int):
    assert isinstance(decimal_number, int) # 해당 구문이 False 인 경우 에러 발생 시킴
    return bin(decimal_number)[2:]

print(get_binary_number(10))
print(get_binary_number(10.0))
```

    1010



    ---------------------------------------------------------------------------
    
    AssertionError                            Traceback (most recent call last)
    
    <ipython-input-13-94541ee5d717> in <module>()
          4 
          5 print(get_binary_number(10))
    ----> 6 print(get_binary_number(10.0))
     
    <ipython-input-13-94541ee5d717> in get_binary_number(decimal_number)
          1 def get_binary_number(decimal_number: int):
    ----> 2     assert isinstance(decimal_number, int) # 해당 구문이 False 인 경우 에러 발생 시킴
          3     return bin(decimal_number)[2:]
          4 
          5 print(get_binary_number(10))
     
    AssertionError: 



## 6.2 File Handling

### 6.2.1 파일의 종류

- 기본적인 파일의 종류로 text 파일과 binary 파일로 나눔
- 컴퓨터는 text 파일을 처리하기 위해 binary 파일로 변환 시킴 (ex. `pyc` 파일)
- 모든 text 파일도 실제는 binary 파일
- ASCII / Unicode 와 같은 데이터 저장 표준을 이용하여 파일을 저장해야 문자열 집합으로 저장되어 사람이 읽을 수 있다.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<img src='https://drive.google.com/uc?id=1dduZ-KFAr_ElymnF1cVJRmEr4jrxMiLF' width=800/>


### 6.2.2 Python File I/O

```python
f = open('<파일이름>', '접근 모드')
f.close()
```

- 접근 모드의 종류
  - `r` : 읽기 모드, 파일을 읽기만 할 때 사용
  - `w`  :쓰기 모드, 파일에 내용을 쓸 때 사용
  - `a` : 추가 모드, 파일의 마지막에 새로운 내용을 추가 시킬 때 사용


### 6.2.3 파이썬의 file read

#### 6.2.3.1 `f.read()`

- txt 파일 안에 있는 내용을 문자열로 반환

```python
f = open('i_have_a_dream.txt', 'r') # 대상 파일이 같은 폴더에 있는 경우
contents = f.read()
print(contents)
f.close()
```

    I am happy to join with you today in what will go down in history as the greatest demonstration for freedom in the history of our nation.
    
    Five score years ago, a great American, in whose symbolic shadow we stand today, signed the Emancipation Proclamation. This momentous decree came as a great beacon light of hope to millions of Negro slaves who had been seared in the flames of withering injustice. It came as a joyous daybreak to end the long night of their captivity.
    
    But one hundred years later, the Negro still is not free. One hundred years later, the life of the Negro is still sadly crippled by the manacles of segregation and the chains of discrimination. One hundred years later, the Negro lives on a lonely island of poverty in the midst of a vast ocean of material prosperity. One hundred years later, the Negro is still languished in the corners of American society and finds himself an exile in his own land. And so we've come here today to dramatize a shameful condition.
    
    ...



- `with` 구문과 함께 사용하기


```python
with open('i_have_a_dream.txt', 'r') as my_file:
    contents = my_file.read()
    print(type(contents), contents)
```

    <class 'str'> I am happy to join with you today in what will go down in history as the greatest demonstration for freedom in the history of our nation.
    
    Five score years ago, a great American, in whose symbolic shadow we stand today, signed the Emancipation Proclamation. This momentous decree came as a great beacon light of hope to millions of Negro slaves who had been seared in the flames of withering injustice. It came as a joyous daybreak to end the long night of their captivity.
    
    But one hundred years later, the Negro still is not free. One hundred years later, the life of the Negro is still sadly crippled by the manacles of segregation and the chains of discrimination. One hundred years later, the Negro lives on a lonely island of poverty in the midst of a vast ocean of material prosperity. One hundred years later, the Negro is still languished in the corners of American society and finds himself an exile in his own land. And so we've come here today to dramatize a shameful condition.
    
    ...



#### 6.2.3.2 `f.readlines()`

- 한 줄 씩 읽어 List Type 으로 반환함


```python
with open('i_have_a_dream.txt', 'r') as my_file:
    content_list = my_file.readlines()
    print(type(content_list))
    print(content_list)
```

    <class 'list'>
    ['I am happy to join with you today in what will go down in history as the greatest demonstration for freedom in the history of our nation.\n', '\n', 'Five score years ago, a great American, in whose symbolic shadow we stand today, signed the Emancipation Proclamation. This momentous decree came as a great beacon light of hope to millions of Negro slaves who had been seared in the flames of withering injustice. It came as a joyous daybreak to end the long night of their captivity.\n',
    ...,
    "And when this happens, and when we allow freedom ring, when we let it ring from every village and every hamlet, from every state and every city, we will be able to speed up that day when all of God's children, black men and white men, Jews and Gentiles, Protestants and Catholics, will be able to join hands and sing in the words of the old Negro spiritual:\n", '\n', '                Free at last! Free at last!\n', '\n', '                Thank God Almighty, we are free at last!']



#### 6.2.3.3 `f.readline()`

- 실행 시 마다 한 줄씩 읽어 오기


```python
with open('i_have_a_dream.txt', 'r') as my_file:
    i = 0
    while True:
        line = my_file.readline()
        if not line:
            break
        print(str(i) + ' === ' + line.replace('\n', ''))
        i += 1
```

    0 === I am happy to join with you today in what will go down in history as the greatest demonstration for freedom in the history of our nation.
    1 === 
    2 === Five score years ago, a great American, in whose symbolic shadow we stand today, signed the Emancipation Proclamation. This momentous decree came as a great beacon light of hope to millions of Negro slaves who had been seared in the flames of withering injustice. It came as a joyous daybreak to end the long night of their captivity.
    3 === 
    4 === But one hundred years later, the Negro still is not free. One hundred years later, the life of the Negro is still sadly crippled by the manacles of segregation and the chains of discrimination. One hundred years later, the Negro lives on a lonely island of poverty in the midst of a vast ocean of material prosperity. One hundred years later, the Negro is still languished in the corners of American society and finds himself an exile in his own land. And so we've come here today to dramatize a shameful condition.
    ...
    83 === 
    84 ===                 Free at last! Free at last!
    85 === 
    86 ===                 Thank God Almighty, we are free at last!



### 6.2.4 파이썬의 File Write

#### 6.2.4.1 mode = 'w'

- mode 는 `w`, `encoding='utf8'`


```python
f = open('count_log.txt', 'w', encoding='utf8')
for i in range(1, 11):
    data = '%d번 째 줄입니다.\n' % i
    f.write(data)
f.close()
```


#### 6.2.4.2 mode = 'a'

- mode = 'a' 는 추가 모드


```python
with open('count_log.txt', 'a', encoding='utf8') as f:
    for i in range(1, 11):
        data = '%d번 째 줄입니다.\n' % i
        f.write(data)
```


### 6.2.5 파이썬의 directory 다루기

#### 6.2.5.1 `os` 활용


```python
import os
os.mkdir('log')
```


```python
try:
    os.mkdir('log')
except FileExistsError as e:
    print(e)
```

    [Errno 17] File exists: 'log'



```python
os.path.exists('log')
```


    True




```python
os.path.exists('abc')
```


    False




```python
os.mkdir('abc')
```


```python
os.path.exists('abc') 
```


    True




```python
if not os.path.isdir('log'): # 디렉토리가 있는 지 확인
    os.mkdir('log')
```


```python
os.path.isfile('file.ipynb')
```


    True




#### 6.2.5.2 `shutil` 을 이용하여 파일 복사


```python
# 파일 옮기기 : shutil 사용
import shutil
source = 'file.ipynb'
dest = os.path.join('abc', 'file.ipynb') # os.path.join : 경로 결합

shutil.copy(source, dest) # shutil.copy() : 파일 복사 함수
```


    'abc/file.ipynb'




#### 6.2.5.3 `pathlib`

- 최근에는 `pathlib` 모듈을 사용하여 path 를 객체로 다룸


```python
import pathlib

cwd = pathlib.Path.cwd()
cwd
```


    PosixPath('/content/drive/My Drive/Colab Notebooks/boostcamp/프리코스/WEEK 2. 파이썬 다지기')




```python
cwd.parent
```


    PosixPath('/content/drive/My Drive/Colab Notebooks/boostcamp/프리코스')




```python
cwd.parent.parent 
```


    PosixPath('/content/drive/My Drive/Colab Notebooks/boostcamp')




```python
list(cwd.parents)
```


    [PosixPath('/content/drive/My Drive/Colab Notebooks/boostcamp/프리코스'),
     PosixPath('/content/drive/My Drive/Colab Notebooks/boostcamp'),
     PosixPath('/content/drive/My Drive/Colab Notebooks'),
     PosixPath('/content/drive/My Drive'),
     PosixPath('/content/drive'),
     PosixPath('/content'),
     PosixPath('/')]




```python
list(cwd.glob('*'))
```


    [PosixPath('/content/drive/My Drive/Colab Notebooks/boostcamp/프리코스/WEEK 2. 파이썬 다지기/003_Exception-File-Log-Handling.ipynb'),
     PosixPath('/content/drive/My Drive/Colab Notebooks/boostcamp/프리코스/WEEK 2. 파이썬 다지기/__pycache__'),
     PosixPath('/content/drive/My Drive/Colab Notebooks/boostcamp/프리코스/WEEK 2. 파이썬 다지기/teamlab_note.py'),
     PosixPath('/content/drive/My Drive/Colab Notebooks/boostcamp/프리코스/WEEK 2. 파이썬 다지기/_img'),
     PosixPath('/content/drive/My Drive/Colab Notebooks/boostcamp/프리코스/WEEK 2. 파이썬 다지기/001_Python Object Oriented Programming (OOP).ipynb'),
     PosixPath('/content/drive/My Drive/Colab Notebooks/boostcamp/프리코스/WEEK 2. 파이썬 다지기/fah_converter.py'),
     PosixPath('/content/drive/My Drive/Colab Notebooks/boostcamp/프리코스/WEEK 2. 파이썬 다지기/module_ex.py'),
     PosixPath('/content/drive/My Drive/Colab Notebooks/boostcamp/프리코스/WEEK 2. 파이썬 다지기/package_ex'),
     PosixPath('/content/drive/My Drive/Colab Notebooks/boostcamp/프리코스/WEEK 2. 파이썬 다지기/002_Module-and-Project.ipynb'),
     PosixPath('/content/drive/My Drive/Colab Notebooks/boostcamp/프리코스/WEEK 2. 파이썬 다지기/i_have_a_dream.txt'),
     PosixPath('/content/drive/My Drive/Colab Notebooks/boostcamp/프리코스/WEEK 2. 파이썬 다지기/count_log.txt'),
     PosixPath('/content/drive/My Drive/Colab Notebooks/boostcamp/프리코스/WEEK 2. 파이썬 다지기/log'),
     PosixPath('/content/drive/My Drive/Colab Notebooks/boostcamp/프리코스/WEEK 2. 파이썬 다지기/file.ipynb'),
     PosixPath('/content/drive/My Drive/Colab Notebooks/boostcamp/프리코스/WEEK 2. 파이썬 다지기/abc')]




### 6.2.6 Log 파일 생성하기

- 디렉토리가 있는 지 확인
- 파일이 있는 지 확인


```python
import os
if not os.path.isdir('log'):
    os.mkdir('log')
if not os.path.exists('log/count_log.txt'):
    f = open('log/count_log.txt', 'w', encoding='utf8')
    f.write('기록이 시작됩니다.\n')
    f.close()

with open('log/count_log.txt', 'a', encoding='utf8') as f:
    import random, datetime
    for i in range(1, 11):
        stamp = str(datetime.datetime.now())
        value = random.random() * 1000000
        log_line = stamp + '\t' + str(value) + '값이 생성되었습니다.' + '\n'
        f.write(log_line)
```


### 6.2.7 `pickle`

- 파이썬의 객체를 영속화(persistence)하는 built-in 객체
- 데이터, object 등 실행 중 정보를 저장 -> 불러와서 사용
- 저장해야 하는 정보, 계산 결과(모델) 등 활용이 많음


```python
# 리스트 저장
import pickle

f = open('list.pickle', 'wb')
test = [1, 2, 3, 4, 5]
pickle.dump(test, f)
f.close()
```


```python
f = open('list.pickle', 'rb')
test_pickle = pickle.load(f)
print(test_pickle)
f.close()
```

    [1, 2, 3, 4, 5]



```python
# 클래스 저장
import pickle

class Multiply(object):
    def __init__(self, multiplier):
        self.multiplier = multiplier

    def multiply(self, number):
        return number * self.multiplier

multiply = Multiply(5)
multiply.multiply(10)
```


    50




```python
f = open('multiply_object.pickle', 'wb')
pickle.dump(multiply, f)
f.close()
```


```python
f = open('multiply_object.pickle', 'rb')
multiply_pickle = pickle.load(f)
multiply_pickle.multiply(5)
```


    25




## 6.3 Logging Handling

### 6.3.1 로그 남기기 - Logging

- 프로그램이 실행되는 동안 일어나는 정보를 기록으로 남기기
- 유저의 접근, 프로그램의 Exception, 특정 함수의 사용
- console 화면에 출력, 파일에 남기기, DB에 남기기 등
- 기록된 로그를 분석하여 의미있는 결과를 도출할 수 있음
- 실행 시점에서 남겨야 하는 기록, 개발 시점에서 남겨야 하는 기록


### 6.3.2 print vs logging

- 기록을 print 로 남기는 것도 가능함
- 그러나 console 창에만 남기는 기록은 분석 시 사용 불가
- 때로는 레벨별(개발, 운영)로 기록을 남길 필요도 있음
- 이러한 기능을 체계적으로 지원하는 모듈이 필요함


### 6.3.3 `logging` 모듈

- Python 의 기본 log 관리 모듈


```python
import logging

logging.debug('틀렸잖아')
logging.info('확인해')
logging.warning('조심해')
logging.error('에러났어')
logging.critical('망했다') # 프로그램이 종료될 때
```

    WARNING:root:조심해
    ERROR:root:에러났어
    CRITICAL:root:망했다


- 기본 logging level 이 warning 이상이기 때문에 warning 부터 출력된다.


### 6.3.4 logging level

- 프로그램 진행 상황에 따라 다른 level 의 log를 출력함
- 개발 시점, 운영 시점 마다 다른 log가 남을 수 있도록 지원함
- DEBUG > INFO > WARNING > ERROR > CRITICAL
- log 관리 시 가장 기본이 되는 설정 정보

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<img src='https://drive.google.com/uc?id=19XWtYJnC0PQMoBjLYg8BNxEEhzDeqwge' width=800/>


### 6.3.5 logging level 지정


```python
import logging

logger = logging.getLogger('main') # Logger 선언
# 출력을 어디에 할 지 지정할 수 있다.
stream_handler = logging.FileHandler(
    'my.log',
    mode='a',
    encoding='utf8'
) # Logger 의 output 방법 선언
logger.addHandler(stream_handler)
```


```python
logger.setLevel(logging.INFO)
logging.debug('틀렸잖아')
logging.info('확인해')
logging.warning('조심해')
logging.error('에러났어')
logging.critical('망했다')
```

    WARNING:root:조심해
    ERROR:root:에러났어
    CRITICAL:root:망했다



```python
logger.setLevel(logging.CRITICAL)
logging.debug('틀렸잖아')
logging.info('확인해')
logging.warning('조심해')
logging.error('에러났어')
logging.critical('망했다')
```

    WARNING:root:조심해
    ERROR:root:에러났어
    CRITICAL:root:망했다



### 6.3.6 logging 설정

- configparser : 파일에 설정
- argparser : 실행 시점에 설정


### 6.3.7 configparser

- 프로그램의 실행 설정을 file에 저장함
- Section, Key, Value 값의 형태로 설정된 설정 파일을 사용
- 설정 파일을 Dict Type 으로 호출 후 사용


#### 6.3.7.1 config file 사용 예시

- Section - 대괄호
- 속성 - key:value or key=value

```
# example.cfg

[SectionOne]
Status: Single
Name: Derek
Value: Yes
Age: 30
Single: True

[SectionTwo]
FavoriteColor = Green

[SectionThree]
FamilyName: Johnson
```


```python
import configparser

config = configparser.ConfigParser()
config.sections()
```


    []




```python
config.read('example.cfg')
config.sections()
```


    ['SectionOne', 'SectionTwo', 'SectionThree']




```python
for key in config['SectionOne']:
    print(key)
```

    status
    name
    value
    age
    single



```python
config['SectionOne']['status']
```


    'Single'




### 6.3.8 argparser

- console 창에서 프로그램 실행 시 setting 정보를 저장함
- 거의 모든 console 기반 python 프로그램 기본으로 제공
- 특수 모듈도 많이 존재하지만(TF), 일반적으로 `argparse`를 사용
- Command-Line Option 이라고 부름
- [https://github.com/abseil/abseil-py](https://github.com/abseil/abseil-py)

- `arg_sum.py` 파일 실행


```python
!python arg_sum.py
```

    usage: arg_sum.py [-h] -a A -b B
    arg_sum.py: error: the following arguments are required: -a/--a_value, -b/--b_value



```python
!python arg_sum.py -a 10 -b 20
```

    Namespace(a=10, b=20)
    10
    20
    30



- 참고용 블로그 : [https://ddiri01.tistory.com/302](https://ddiri01.tistory.com/302)


### 6.3.9 Logging formatter

- Log의 결과값의 format을 지정해줄 수 있음

```python
formatter = logging.Formatter('%(asctime)s %(levelname)s %(process)d %(message)s') 
```

