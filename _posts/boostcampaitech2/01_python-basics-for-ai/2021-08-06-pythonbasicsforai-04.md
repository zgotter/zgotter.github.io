---
layout: post
title: "[Python Basics for AI] 4. 파이썬 객체 지향 프로그래밍"
image: /assets/img/boostcampaitech2/cover.png
accent_image: 
  background: url('/assets/img/boostcampaitech2/cover.png') center/cover
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
description: >
  파이썬 객체 지향 프로그래밍
categories:
  - boostcampaitech2
  - pythonbasicsforai
author: zgotter
sitemap: false
published: true
comments: true
---

# 4. [Python Basics for AI] 4. 파이썬 객체 지향 프로그래밍

* 0.
{:toc}

## 4.1 파이썬 클래스 구현

### 4.1.1 파이썬에서 `__` 의 의미

- `__` 는 특수한 예약 함수나 변수 그리고 함수명 변경(맨글링)으로 사용
- magic method 예시
  - `__init__` : 객체 초기화 예약 함수
  - `__main__`
  - `___add__`
  - `__str__` : 해당 객체의 print() 함수
  - `__eq__`


```python
class SoccerPlayer(object):
    def __init__(self, name: str, position: str, back_number: int):
        self.name = name
        self.position = position
        self.back_number = back_number

    def change_back_number(self, new_number):
        print('선수의 등번호를 변경합니다. : From %d to %d' % (self.back_number, new_number))
        self.back_number = new_number

    def __str__(self): # 해당 객체의 print() 반환값
        return "Hello, My Name is %s. I play in %s in center " % (self.name, self.position)

    def __add__(self, other): # 
        return self.name + other.name
```


```python
son = SoccerPlayer('son', 'FW', 7)
park = SoccerPlayer('park', 'MF', 13)
print(son)
print(park)
```

    Hello, My Name is son. I play in FW in center 
    Hello, My Name is park. I play in MF in center 



```python
print(son + park)
```

    sonpark



### 4.1.2 method 구현

- 반드시 `self` 를 추가해야만 class 함수로 인정됨


### 4.1.3 objects(instance) 사용

- `self` : 생성된 인스턴스 자기 자신을 의미한다.


## 4.2 OOP Implementation Example

### 4.2.1 노트북

- Note 를 정리하는 프로그램
- 사용자는 Note에 뭔가를 적을 수 있다.
- Note에는 Content 가 있고, 내용을 제거할 수 있다.
- 두 개의 노트북을 합쳐 하나로 만들 수 있다.
- Note는 Notebook에 삽입된다.
- Notebook은 Note가 삽입될 때 페이지를 생성하며, 최고 300페이지까지 저장 가능하다.
- 300 페이지가 넘으면 더 이상 노트를 삽입하지 못한다.

```python
# teamlab_note.py
class Note:
    def __init__(self, content=None):
        self.content = content

    def write_content(self, content):
        self.content = content

    def remove_all(self):
        self.content = ''

    def __add__(self, other):
        return self.content + other.content

    def __str__(self):
        return f"노트에 적힌 내용입니다.: {self.content}"

class Notebook:
    def __init__(self, title):
        self.title = title
        self.page_number = 1
        self.notes = {}

    def add_note(self, note, page=0):
        if self.page_number <= 300:
            if page == 0:
                self.notes[self.page_number] = note
                self.page_number += 1
            else:
                self.notes[page] = note
        else:
            print('Page가 모두 채워졌습니다.')
    
    def remove_note(self, page_number):
        if page_number in self.notes.keys():
            return self.notes.pop(page_number)
        else:
            print('해당 페이지는 존재하지 않습니다.')

    def get_number_of_pages(self):
        return len(self.notes.keys())
```

```python
from teamlab_note import Note
from teamlab_note import Notebook
```


```python
my_notebook = Notebook('팀랩 강의노트')
my_notebook
```




    <teamlab_note.Notebook at 0x7f8e0ba20450>




```python
new_note = Note('아 수업하기 싫다.')
print(new_note)
```

    노트에 적힌 내용입니다.: 아 수업하기 싫다.



```python
new_note_2 = Note('파이썬 강의')
print(new_note_2)
```

    노트에 적힌 내용입니다.: 파이썬 강의



```python
my_notebook.add_note(new_note)
my_notebook.add_note(new_note_2, 100)
```


```python
my_notebook.get_number_of_pages()
```




    2




```python
print(my_notebook.notes[1])
```

    노트에 적힌 내용입니다.: 아 수업하기 싫다.



```python
print(my_notebook.notes[100])
```

    노트에 적힌 내용입니다.: 파이썬 강의



```python
my_notebook.notes[2] = Note('안녕')
```


```python
print(my_notebook.notes[2])
```

    노트에 적힌 내용입니다.: 안녕


## 4.3 OOP characteristics

- Inheritance : 상속
- Polymorphism : 다형성
- Visibility : 가시성


### 4.3.1 상속 (Inheritance)

- 부모 클래스로부터 속성과 Method를 물려받은 자식 클래스를 생성하는 것
- 자식 클래스에서 `super()` 를 통해 부모 클래스의 메서드를 호출할 수 있다.


```python
class Person(object):
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __str__(self):
        return f"저의 이름은 {self.name} 입니다. 나이는 {self.age} 입니다."
```


```python
class Korean(Person):
    pass
```


```python
first_korean = Korean('Sunghan', 31)
print(first_korean.name)
```

    Sunghan



```python
# 부모 클래스 Person 선언
class Person:
    def __init__(self, name, age, gender):
        self.name = name
        self.age = age
        self.gender = gender

    def about_me(self):
        print(f"저의 이름은 {self.name} 이구요, 제 나이는 {self.age}살 입니다.")

    def __str__(self):
        return f"저의 이름은 {self.name} 이구요, 제 나이는 {self.age}살 입니다."    
```


```python
# 부모 클래스 Person으로부터 상속
class Employee(Person):
    def __init__(self, name, age, gender, salary, hire_date):
        super().__init__(name, age, gender) # super() 를 이용하여 부모 객체 사용
        self.salary = salary
        self.hire_date = hire_date # 속성값 추가

    def do_work(self): # 새로운 메서드 추가
        print('열심히 일을 합니다.')

    def about_me(self): # 부모 클래스 함수 재정의
        super().about_me() # 부모 클래스 함수 사용
        print(f"제 급여는 {self.salary}원 이구요, 제 입사일은 {self.hire_date} 입니다.")
```


```python
myPerson = Person('John', 34, 'Male')
myEmployee = Employee('Daeho', 34, 'Male', 300000, '2012/03/01')
```


```python
myPerson.about_me()
```

    저의 이름은 John 이구요, 제 나이는 34살 입니다.



```python
myEmployee.about_me()
```

    저의 이름은 Daeho 이구요, 제 나이는 34살 입니다.
    제 급여는 300000원 이구요, 제 입사일은 2012/03/01 입니다.



### 4.3.2 다형성 (Polymorphism)

- 같은 이름 메소드의 내부 로직을 다르게 작성
- Dynamic Typing 특성으로 인해 파이썬에서는 같은 부모 클래스의 상속에서 주로 발생함
- 중요한 OOP 개념, 그러나 너무 깊이 알 필요 없다.


```python
class Animal:
    def __init__(self, name):
        self.name = name

    def talk(self):
        raise NotImplementedError('Subclass must implement abstract method')
```


```python
class Cat(Animal):
    def talk(self):
        return 'Meow!'
```


```python
class Dog(Animal):
    def talk(self):
        return 'Woof!'
```


```python
animals = [
    Cat('Missy'),
    Cat('Mr. Mistoffelees'),
    Dog('Lassie')
]

for animal in animals:
    print(animal.name + ': ' + animal.talk())
```

    Missy: Meow!
    Mr. Mistoffelees: Meow!
    Lassie: Woof!



### 4.3.3 가시성 (Visibility)

#### 4.3.3.1 visibility overview

- 객체의 정보를 볼 수 있는 레벨을 조절하는 것
- **누구나 객체 안에 모든 변수를 볼 필요가 없음**
  - 객체를 사용하는 사용자가 임의로 정보 수정
  - 필요 없는 정보에는 접근할 필요가 없음
  - 만약 제품으로 판매한다면? 소스의 보호


#### 4.3.3.2 캡슐화 (Encapsulation) or 정보 은닉 (Information Hiding)

- class를 설계할 때, 클래스 간 간섭/정보공유의 최소화
- 캡슐을 던지듯, 인터페이스만 알아서 써야 함


#### 4.3.3.3 Visibility Example 1

- Product 객체를 Inventory 객체에 추가
- Inventory 에는 오직 Product 객체만 들어감
- Inventory 에 Product 가 몇 개인지 확인 필요
- Inventory 에 Product items 는 직접 접근이 불가


```python
class Product:
    pass
```


```python
class Inventory:
    def __init__(self):
        self.__items = [] # "__" 를 변수명 앞에 붙임으로서 private 변수로 선언, 타 객체가 접근 못함

    def add_new_item(self, product):
        if type(product) == Product:
            self.__items.append(product)
            print('new item added')
        else:
            raise ValueError('Invalid Item')

    def get_number_of_items(self):
        return len(self.__items)
```


#### 4.3.3.4 Visibility Example 2

- Product 객체를 Inventory 객체에 추가
- Inventory 에는 오직 Product 객체만 들어감
- Inventory 에 Product 가 몇 개인지 확인 필요
- Inventory 에 Product **items 접근 허용**


```python
class Inventory:
    def __init__(self):
        self.__items = [] # "__" 를 변수명 앞에 붙임으로서 private 변수로 선언, 타 객체가 접근 못함

    @property # property decorator : 숨겨진 변수를 반환하게 해줌
    def items(self):
        return self.__items

    def add_new_item(self, product):
        if type(product) == Product:
            self.__items.append(product)
            print('new item added')
        else:
            raise ValueError('Invalid Item')

    def get_number_of_items(self):
        return len(self.__items)
```


```python
my_inventory = Inventory()
my_inventory.add_new_item(Product())
my_inventory.add_new_item(Product())
print(my_inventory.get_number_of_items())
```

    new item added
    new item added
    2



```python
items = my_inventory.items # Property decorator로 함수를 변수처럼 호출
items.append(Product())
print(my_inventory.get_number_of_items())
```

    3



## 4.4 decorate

### 4.4.1 decorator 를 이해하기 위한 개념들

- first-class objects
- inner function
- decorator


### 4.4.2 First-class objects

- 일등함수 or 일급 객체
- 변수나 데이터 구조에 할당이 가능한 객체
- 파라미터로 전달이 가능 + 리턴 값으로 사용
- **파이썬의 함수는 일급 함수이다.**


```python
def square(x):
    return x*x

f = square # 함수를 변수로 사용
f(5)
```




    25




```python
def square(x):
    return x*x

def cube(x):
    return x*x*x

def formula(method, argument_list): # method : 함수를 파라미터로 사용
    return [method(value) for value in argument_list]

f = square
g = cube

lst = [1,2,3,4]
print(formula(f, lst))
print(formula(g, lst))
```

    [1, 4, 9, 16]
    [1, 8, 27, 64]



### 4.4.3 inner function

- 함수 내에 또 다른 함수가 존재


```python
def print_msg(msg):
    def printer():
        print(msg)
    printer()

print_msg('Hello, Python')
```

    Hello, Python



### 4.4.4 closures

- inner function을 return 값으로 반환
- 파이썬의 함수가 일급 객체이기 때문에 함수를 반환할 수 있어서 closures 를 할 수 있다.
- 비슷한 목적을 갖는 다양한 변형이 되어 있는 함수들을 만들어 낼 수 있다.


```python
def print_msg(msg):
    def printer():
        print(msg)
    return printer

another = print_msg('Hello, Python') # inner function 이 반환된다.
another()
```

    Hello, Python



```python
# closure example
def tag_func(tag, text):
    text = text
    tag = tag

    def inner_func():
        return f"<{tag}>{text}</{tag}>"

    return inner_func

h1_func = tag_func('title', 'This is Python_Class')
p_func = tag_func('p', 'Data Academy')

print(h1_func())
print(p_func())
```

    <title>This is Python_Class</title>
    <p>Data Academy</p>



### 4.4.5 decorator function

- 복잡한 closure 함수를 간단하게!


```python
def star(func):
    def inner(*args, **kwargs):
        print('*'*30)
        func(*args, **kwargs)
        print('*'*30)
    return inner

@star # star decorator 아래에 정의된 함수가 위에서 정의한 star 함수의 func 파라미터로 들어가게 된다.
def printer(msg):
    print(msg)

printer('Hello')
```

    ******************************
    Hello
    ******************************



```python
def star(func):
    def inner(*args, **kwargs):
        print(args[1]*30)
        func(*args, **kwargs)
        print(args[1]*30)
    return inner

@star # star decorator 아래에 정의된 함수가 위에서 정의한 star 함수의 func 파라미터로 들어가게 된다. printer 함수를 star decorator 로 꾸며주는 것이다.
def printer(msg, mark):
    print(msg)

printer('Hello', '*')
```

    ******************************
    Hello
    ******************************



```python
def star(func):
    def inner(*args, **kwargs):
        print(args[1]*30)
        func(*args, **kwargs)
        print(args[1]*30)
    return inner

@star # star decorator 아래에 정의된 함수가 위에서 정의한 star 함수의 func 파라미터로 들어가게 된다.
def printer(msg, mark):
    print(msg)

printer('Hello', '#')
```

    ##############################
    Hello
    ##############################



```python
# deccrator 에 파라미터를 사용하기 위해서는 inner function 으로 wrapper 를 사용하여 한번 감싸줘야 한다.
def generate_power(exponent): # exponent : decorator 파라미터 (= 2)
    def wrapper(f): # f : decorator 아래 정의된 함수
        def inner(*args):
            result = f(*args) # 7**2 = 49
            return exponent**result # 2**49
        return inner
    return wrapper

@generate_power(2)
def raise_two(n):
    return n**2

print(raise_two(7))
```

    562949953421312
