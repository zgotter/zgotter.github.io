---
layout: post
title: "[Python Basics for AI] 5. Module and Project"
image: /assets/img/boostcampaitech2/cover.png
accent_image: 
  background: url('/assets/img/boostcampaitech2/cover.png') center/cover
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
description: >
  Module and Project
categories:
  - boostcampaitech2
  - pythonbasicsforai
author: zgotter
sitemap: false
published: true
comments: true
---

# 5. [Python Basics for AI] 5. Module and Project

* 0.
{:toc}

## 5.1 모듈과 패키지

### 5.1.1 모듈 (Module)

- 어떤 대상의 부분 혹은 조각
- 프로그램에서는 작은 프로그램 조각들
- 모듈들을 모아서 하나의 큰 프로그램을 개발함
- 프로그램을 모듈화 시키면 다른 프로그램이 사용하기 쉬움
  - ex) 카카오톡 게임을 위한 카카오톡 접속 모듈


### 5.1.2 모듈 in Python

- Built-in Module 인 `random` 을 사용하여 난수를 쉽게 생성할 수 있음


### 5.1.3 패키지

- 모듈을 모아높은 단위
- 하나의 프로그램


## 5.2 모듈 (Module)

### 5.2.1 모듈(Module) 만들기

- 파이썬의 Module은 py 파일을 의미
- 같은 폴더에 Module 에 해당하는 .py 파일과 사용하는 .py 파일을 저장한 후 import 문을 사용해서 module 호출

- 실습 파일
  - `fah_converter.py`
  - `module_ex.py`


### 5.2.2 `__pycache__`

- 모듈을 호출하게 되면 해당 경로에 `__pycache__` 라는 폴더가 생긴다.
- 여기에는 컴파일된 파일이 위치하게 된다.


### 5.2.3 namespace

- 모듈을 호출할 때 범위를 정하는 방법
- 모듈 안에는 함수와 클래스 등이 존재할 수 있다.
- 이 중 필요한 내용만 골라서 호출할 수 있음
- from 과 import 키워드를 사용함


### 5.2.4 namespace example

- Alias 설정 - 모듈명을 별칭으로 써서 사용 (해당 방식 선호, 어디서 나왔는 지 알 수 있음)
  - `import fah_converter as fah`
- 모듈에서 특정 함수 또는 클래스만 호출
  - `from fah_converter import convert_c_to_f`
- 모듈에서 모든 함수 또는 클래스 호출
  - `from fah_converter import *`


### 5.2.5 Built-in Modules

- 난수
  - `import random`
  - `random.randint(0,100)` : 0~100 사이 정수 난수 생성
  - `random.random()` : 일반적인 난수 생성
- 시간
  - `import time`
  - `time.localtime()` : 현재 시간 출력
- 웹
  - `import urllib.request`
  - `response = urllib.request.urlopen('http://tehtemlab.io')`
  - `print(response.head())`


## 5.3 패키지

### 5.3.1 패키지 overview

- 하나의 대형 프로젝트를 만드는 코드의 묶음
- 다양한 모듈들의 합, 폴더로 연결됨
- `__init__`, `__main__` 등 키워드 파일명이 사용됨
- 다양한 오픈 소스들이 모두 패키지로 관리됨


### 5.3.2 패키지 만들기

#### 5.3.2.1 폴더 생성

- 기능들을 세부적으로 나눠 폴더로 만듦
```
game
  ㄴ image
  ㄴ sound
  ㄴ stage  
```


#### 5.3.2.2 폴더별 모듈 구현

- 각 폴더별로 필요한 모듈을 구현

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<img src='https://drive.google.com/uc?id=1pVYkaV2Kdnupou1xnoG-RYd-2yEihp4h' width=600/>


- 각각의 폴더에는 `__init__.py` 라는 파일이 있어야 한다.
  - `touch __init__.py` 명령어를 통해 해당 파일을 생성할 수 있다.
  - 탐색기에서 직접 .py 파일을 생성할 수 도 있다.


#### 5.3.2.3 1차 test

- python shell 을 이용하여 테스트
- `game` 폴더에서 실행하여 테스트를 한다.
```python
from sound import echo
echo.echo_play()
```


#### 5.3.2.4 `__init__.py`

- 현재 폴더가 패키지임을 알리는 초기화 스크립트
- 없을 경우 패키지로 간주하지 않음
  - python 3.3 이상에서는 해당 파일을 생성하지 않아도 된다.
- 해당 파일 안에는 하위 폴더와 py 파일(모듈)을 모두 포함함
- `import` 와 `__all__` keyword 사용

```python
# game 폴더의 __init__.py 내용
__all__ = ['image', 'sound', 'stage'] # 사용할 모듈들의 이름을 리스트로 할당
 
from . import image
from . import sound
from . import stage
```

```python
# game/image 폴더의 __init__.py 내용
__all__ = ['character', 'object_type']
 
from . import character
from . import object_type
```

```python
# game/sound 폴더의 __init__.py 내용
__all__ = ['bgm', 'echo']
 
from . import bgm
from . import echo
```

```python
# game/stage 폴더의 __init__.py 내용
__all__ = ['main', 'sub']
 
from . import main
from . import sub
```


#### 5.3.2.5 `__main__.py`

- 프로젝트(패키지)를 실행시키기 위한 파일
- root 폴더(game) 하위에 생성
- 필요한 내용 작성
- 해당 파일 생성 후 `package_ex` 폴더에서 다음 명령어 실행 시 game 패키지가 호출됨
  - `python game`


### 5.3.3 package namespace

- package 내에서 다른 폴더의 모듈을 부를 때 상대 참조로 호출

- 절대 참조
  - `from game.grahpic.render import render_test`
- `.` : 현재 디렉토리 기준
  - `from .render import render_test`
- `..` : 부모 디렉토리 기준
  - `from ..sound.echo import echo_test`


## 5.4 가상 환경

### 5.4.1 가상 환경 생성

```
conda create -n 가상환경이름 python=파이썬버전
```

```
conda create -n my_project python=3.8
```


### 5.4.2 가상환경 패키지 설치

```
conda install 패키지명
```

```
conda install matplotlib
```

- windows -> `conda`
- linux, mac -> `conda` or `pip`

- windows 에서는 컴파일된 C 라이브러리 설치 필요 (`[vc10]`)
  - `conda`는 c 라이브러리를 같이 설치해준다.


### 5.4.3 가상 환경 예시

- `matplotlib`
- `tqdm`