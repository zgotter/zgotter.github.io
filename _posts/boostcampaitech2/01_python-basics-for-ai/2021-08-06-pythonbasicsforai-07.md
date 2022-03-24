---
layout: post
title: "[Python Basics for AI] 7. Python data handling"
image: /assets/img/boostcampaitech2/cover.png
accent_image: 
  background: url('/assets/img/boostcampaitech2/cover.png') center/cover
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
description: >
  Python data handling
categories:
  - boostcampaitech2
  - pythonbasicsforai
author: zgotter
sitemap: false
published: true
comments: true
---

# 7. [Python Basics for AI] 7. Python data handling

* 0.
{:toc}

## 7.1 CSV (Comma Separate Values)

- 엑셀 양식의 데이터를 프로그램에 상관없이 쓰기 위한 데이터 형식
- 탭(TSV), 빈칸(SSV) 등으로 구분해서 만들기도 함



### 7.1.1 파이썬으로 CSV 파일 읽기/쓰기

- Text 파일 형태로 데이터 처리 예제
- 예제 데이터 : customer.csv ([https://bit.ly/3psoUZb](https://bit.ly/3psoUZb))
- 일반적 textfile을 처리하듯 파일을 읽어온 후, 한줄씩 데이터를 처리함




#### 7.1.1.1 csv 파일 읽기 예제


```python
line_counter = 0 # 파일의 총 줄수를 세는 변수
data_header = [] # data의 필드값을 저장하는 list
customer_list = [] # customer 개별 list를 저장하는 list

with open('customers.csv') as customer_data:
    while True:
        data = customer_data.readline()
        if not data: break
        if line_counter == 0: # 첫 번째 데이터는 데이터의 필드
            data_header = data.split(',')
        else:
            customer_list.append(data.split(','))
        line_counter += 1

print('Header :\t', data_header)
for i in range(10):
    print('data',i,':\t\t', customer_list[i])
print(len(customer_list))
```

    Header :	 ['customerNumber', 'customerName', 'contactLastName', 'contactFirstName', 'phone', 'addressLine1', 'addressLine2', 'city', 'state', 'postalCode', 'country', 'salesRepEmployeeNumber', 'creditLimit\n']
    data 0 :		 ['103', '"Atelier graphique"', 'Schmitt', '"Carine "', '40.32.2555', '"54', ' rue Royale"', 'NULL', 'Nantes', 'NULL', '44000', 'France', '1370', '21000\n']
    data 1 :		 ['112', '"Signal Gift Stores"', 'King', 'Jean', '7025551838', '"8489 Strong St."', 'NULL', '"Las Vegas"', 'NV', '83030', 'USA', '1166', '71800\n']
    data 2 :		 ['114', '"Australian Collectors', ' Co."', 'Ferguson', 'Peter', '"03 9520 4555"', '"636 St Kilda Road"', '"Level 3"', 'Melbourne', 'Victoria', '3004', 'Australia', '1611', '117300\n']
    data 3 :		 ['119', '"La Rochelle Gifts"', 'Labrune', '"Janine "', '40.67.8555', '"67', ' rue des Cinquante Otages"', 'NULL', 'Nantes', 'NULL', '44000', 'France', '1370', '118200\n']
    data 4 :		 ['121', '"Baane Mini Imports"', 'Bergulfsen', '"Jonas "', '"07-98 9555"', '"Erling Skakkes gate 78"', 'NULL', 'Stavern', 'NULL', '4110', 'Norway', '1504', '81700\n']
    data 5 :		 ['124', '"Mini Gifts Distributors Ltd."', 'Nelson', 'Susan', '4155551450', '"5677 Strong St."', 'NULL', '"San Rafael"', 'CA', '97562', 'USA', '1165', '210500\n']
    data 6 :		 ['125', '"Havel & Zbyszek Co"', 'Piestrzeniewicz', '"Zbyszek "', '"(26) 642-7555"', '"ul. Filtrowa 68"', 'NULL', 'Warszawa', 'NULL', '01-012', 'Poland', 'NULL', '0\n']
    data 7 :		 ['128', '"Blauer See Auto', ' Co."', 'Keitel', 'Roland', '"+49 69 66 90 2555"', '"Lyonerstr. 34"', 'NULL', 'Frankfurt', 'NULL', '60528', 'Germany', '1504', '59700\n']
    data 8 :		 ['129', '"Mini Wheels Co."', 'Murphy', 'Julie', '6505555787', '"5557 North Pendale Street"', 'NULL', '"San Francisco"', 'CA', '94217', 'USA', '1165', '64600\n']
    data 9 :		 ['131', '"Land of Toys Inc."', 'Lee', 'Kwai', '2125557818', '"897 Long Airport Avenue"', 'NULL', 'NYC', 'NY', '10022', 'USA', '1323', '114900\n']
    122




#### 7.1.1.2 csv 파일 쓰기 예제



### 7.1.2 CSV 객체로 CSV 처리

- Text 파일 형태로 데이터 처리 시 문장 내에 들어가 있는 "," 등에 대해 전처리 과정 필요
- 파이썬에서는 간단히 CSV 파일을 처리하기 위해 **csv 객체**를 제공함
- 예제 데이터 : `korea_food_traffic_data.csv` ([http://www.data.go.kr](http://www.data.go.kr))
  - 국내 주요 상권의 유동인구 현황 정보
  - 한글로 되어 있어 한글 처리 필요



#### 7.1.2.1 csv 객체 활용

```python
import csv

reader = csv.reader(
    f, # 파일 객체
    delimiter=',', # 글자를 나누는 기준
    lineterminator='\r\n', # 줄 바꿈 기준
    quotechar='"', # 문자열을 둘러싸는 신호 문자
    quoting=csv.QUOTE_ALL # 데이터를 나누는 기준이 quotechar에 의해 둘러싸인 레벨
)
```

- 참고 : Windows 에서는 encoding 형식을 `cp949`를 사용한다. (왠만한 데이터는 `utf8`로 바꿔서 사용하는 것이 좋다.)



## 7.2 HTML (Hyper Text Markup Language)

### 7.2.1 정규식 (regular expression)

- 정규 표현식, regexp 또는 regex 등으로 불림
- 복잡한 문자열 패턴을 정의하는 문자 표현 공식
- 특정한 규칙을 가진 문자열의 집합을 추출

```regex
010-0000-0000 ^\d{3}\-\d{4}\-\d{4}$
203.252.101.40 ^\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}$
```



### 7.2.2 정규식 for HTML Parsing

- 주민등록번호, 전화번호, 도서 ISBN 등 형식이 있는 문자열을 원본 문자열로부터 추출함
- HTML 역시 tag를 사용한 일정한 형식이 존재하여 정규식으로 추출이 용이함
- 관련 자료 : [http://www.nextree.co.kr/p4327](http://www.nextree.co.kr/p4327)

- 문법 자체는 매우 방대, 스스로 찾아서 하는 공부 필요



### 7.2.3 정규식 연습장 활용하기

- [http://www.regexr.com](http://www.regexr.com)



### 7.2.4 정규식 기본 문법

#### 7.2.4.1 메타 문자

- 정규식 표현을 위해 원래 의미가 아닌 다른 용도로 사용되는 문자
```
. ^ $ * + ? { } [ ] \ | ( )
```

- `.` : 줄바꿈 문자인 `\n`을 제외한 모든 문자와 매치
- `*` : 앞에 있는 글자를 반복해서 나올 수 있음
  - `tomor*ow` : tomorrow, tomoow, tomorrrrow
- `+` : 앞에 있는 글자를 최소 1회 이상 반복
- `{m,n}` : 반복 횟수를 지정
  - 203.252.101.40 : `[0-9]{1,3}`, `\d{1,3}`
- `?` : 반복 횟수가 1회
- `|` : or
- `^` : not



### 7.2.5 정규식 추출 연습

- 정규식 연습장([http://www.regexr.com](http://www.regexr.com))으로 이동
- 구글 USPTO Bulk Download 데이터 페이지 소스 보기 클릭
  - [http://www.google.com/googlebooks/uspto-patents-grants-text.html](http://www.google.com/googlebooks/uspto-patents-grants-text.html)
- 소스 전체 복사 후 정규식 연습장 페이지에 붙여넣기
- 상단 Expression 부분을 수정해가며 "Zip"로 끝나는 파일명만 추출
- Expression에 `(http)(.+)(zip)` 를 입력



### 7.2.6 정규식 in 파이썬

- `re` 모듈을 import 하여 사용
- 함수
  - `search` : 한 개만 찾기
  - `findall` : 전체 찾기
- 추출된 패턴은 tuple로 반환됨



#### 7.2.6.1 연습 1

- 특정 페이지에서 ID 만 추출하기 ([https://bit.ly/3rxQFS4](https://bit.ly/3rxQFS4))
- ID 패턴 : `[영문대소문자|숫자]` 여러 개, 별표로 끝남
  - `[A-Za-z0-9]+\*\*\*`

```python
import re
import urllib.request

url = 'https://bit.ly/3rxQFS4'
html = urllib.request.urlopen(url)
html_contents = str(html.head())
id_results = re.findall(r"[A-Za-z0-9]+\*\*\*", html_contents)

for result in id_results:
    print(result)
```



#### 7.2.6.2 연습 2


```python
import urllib.request
import re

url = 'http://www.google.com/googlebooks/uspto-patents-grants-text.html'
html = urllib.request.urlopen(url)
html_contents = str(html.read().decode('utf8'))

url_list = re.findall(r'(http)(.+)(zip)', html_contents)
for url in url_list:
    print(''.join(url))
```



### 7.2.7 정규식 in 파이썬 for html

```
<dl class="blind">
    <dt>종목 시세 정보</dt>
    <dd>2021년 07월 23일 16시 10분 기준 장마감</dd>
    <dd>종목명 삼성전자</dd>
    <dd>종목코드 005930 코스피</dd>
    <dd>현재가 79,300 전일대비 하락 400 마이너스 0.50 퍼센트</dd>
    <dd>전일가 79,700</dd>
    <dd>시가 79,700</dd>
    <dd>고가 79,900</dd>
    <dd>상한가 103,500</dd>
    <dd>저가 79,200</dd>
    <dd>하한가 55,800</dd>
    <dd>거래량 8,976,997</dd>
    <dd>거래대금 713,707백만</dd>
</dl>
```

- `<dl class="blind"> ~~~ </dl>` 에 있는
  - `(\<dl class=\"blind\"\>)([\s\S]+?)(\<\/dl\>)`
- `<dd> ~~~ </dd>` 정보를 추출
  - `(\<dd\>)([\s\S]+?)(\<\/dd\>)`


```python
import urllib.request
import re

url = 'http://finance.naver.com/item/main.nhn?code=005930'
html = urllib.request.urlopen(url)
html_contents = str(html.read().decode('ms949'))
```


```python
stock_results = re.findall('(\<dl class=\"blind\"\>)([\s\S]+?)(\<\/dl\>)', html_contents)
print(stock_results)
```

    [('<dl class="blind">', '\n\t        <dt>종목 시세 정보</dt>\n\t        <dd>2021년 07월 23일 16시 10분 기준 장마감</dd>\n\t        <dd>종목명 삼성전자</dd>\n\t        <dd>종목코드 005930 코스피</dd>\n\t        <dd>현재가 79,300 전일대비 하락 400 마이너스 0.50 퍼센트</dd>\n\t        <dd>전일가 79,700</dd>\n\t        <dd>시가 79,700</dd>\n\t        <dd>고가 79,900</dd>\n\t        <dd>상한가 103,500</dd>\n\t        <dd>저가 79,200</dd>\n\t        <dd>하한가 55,800</dd>\n\t        <dd>거래량 8,976,997</dd>\n\t        <dd>거래대금 713,707백만</dd>\n        ', '</dl>'), ('<dl class="blind">', '\n                        <dt><strong>삼성전자</strong></dt>\n                        <dd>오늘의시세 79,300 포인트</dd>\n                        <dd>400 포인트 하락</dd>\n                        <dd>0.50% 마이너스</dd>\n                ', '</dl>')]



```python
samsung_stock = stock_results[0]
samsung_stock
```


    ('<dl class="blind">',
     '\n\t        <dt>종목 시세 정보</dt>\n\t        <dd>2021년 07월 23일 16시 10분 기준 장마감</dd>\n\t        <dd>종목명 삼성전자</dd>\n\t        <dd>종목코드 005930 코스피</dd>\n\t        <dd>현재가 79,300 전일대비 하락 400 마이너스 0.50 퍼센트</dd>\n\t        <dd>전일가 79,700</dd>\n\t        <dd>시가 79,700</dd>\n\t        <dd>고가 79,900</dd>\n\t        <dd>상한가 103,500</dd>\n\t        <dd>저가 79,200</dd>\n\t        <dd>하한가 55,800</dd>\n\t        <dd>거래량 8,976,997</dd>\n\t        <dd>거래대금 713,707백만</dd>\n        ',
     '</dl>')




```python
samsung_index = samsung_stock[1]
samsung_index
```


    '\n\t        <dt>종목 시세 정보</dt>\n\t        <dd>2021년 07월 23일 16시 10분 기준 장마감</dd>\n\t        <dd>종목명 삼성전자</dd>\n\t        <dd>종목코드 005930 코스피</dd>\n\t        <dd>현재가 79,300 전일대비 하락 400 마이너스 0.50 퍼센트</dd>\n\t        <dd>전일가 79,700</dd>\n\t        <dd>시가 79,700</dd>\n\t        <dd>고가 79,900</dd>\n\t        <dd>상한가 103,500</dd>\n\t        <dd>저가 79,200</dd>\n\t        <dd>하한가 55,800</dd>\n\t        <dd>거래량 8,976,997</dd>\n\t        <dd>거래대금 713,707백만</dd>\n        '




```python
index_list = re.findall('(\<dd\>)([\s\S]+?)(\<\/dd\>)', samsung_index)

for index in index_list:
    print(index[1])
```

    2021년 07월 23일 16시 10분 기준 장마감
    종목명 삼성전자
    종목코드 005930 코스피
    현재가 79,300 전일대비 하락 400 마이너스 0.50 퍼센트
    전일가 79,700
    시가 79,700
    고가 79,900
    상한가 103,500
    저가 79,200
    하한가 55,800
    거래량 8,976,997
    거래대금 713,707백만




## 7.3 XML (eXtensible Markup Language)

### 7.3.1 XML 이란

- 데이터의 구조와 의미를 설명하는 TAG(Markup)를 사용하여 표시하는 언어
- TAG와 TAG 사이에 값이 표시되고, 구조적인 정보를 표현할 수 있음
- 정보의 구조에 대한 정보인 스키마와 DTD 등으로 정보에 대한 정보(메타정보)가 표현되며, 용도에 따라 다양한 형태로 변경 가능
- XML은 컴퓨터(ex. PC <-> 스마트폰)간에 정보를 주고받기 매우 유용한 저장 방식으로 쓰이고 있음



### 7.3.2 XML 예제



### 7.3.3 XML Parsing in Python

- XML 도 정규표현식으로 Parsing 이 가능함
- 그러나 좀 더 손쉬운 도구들이 개발되어 있음
- 가장 많이 쓰이는 parser인 `beautifulsoup` 으로 파싱



### 7.3.4 BeautifulSoup

- HTML, XML 등 Markup 언어 Scraping 을 위한 대표적인 도구
- `lxml` 과 `html5lib` 과 같은 parser를 사용함
- 속도는 상대적으로 느리나 간편히 사용할 수 있음



### 7.3.5 beautifulSoup 모듈 사용

```python
# 모듈 호출
from bs4 import BeautifulSoup

# 객체 생성
soup = BeautifulSoup(books_xml, 'lxml')

# tag를 찾는 함수 find_all
soup.find_all('author')
```

- `find_all()` : 정규식과 마찬가지로 해당 패턴을 모두 반환
- `get_text()` : 반환된 패턴의 값 반환 (태그와 태그 사이의 값)


```python
from bs4 import BeautifulSoup

with open('books.xml', 'r', encoding='utf8') as books_file:
    books_xml = books_file.read()

soup = BeautifulSoup(books_xml, 'lxml')

for book_info in soup.find_all('author'):
    print(book_info)
    print(book_info.get_text())
```

    <author>Carson</author>
    Carson
    <author>Sungchul</author>
    Sungchul




## 7.4 JSON (JavaScript Object Notation)

### 7.4.1 JSON Overview

- 원래 웹 언어인 JavaScript 의 데이터 객체 표현 방식
- 간결성으로 기계/인간이 모두 이해하기 편함
- 데이터 용량이 적고, code로의 전환이 쉬움
- 이로 인해 XML의 대체제로 많이 활용되고 있음



### 7.4.2 Sample JSON Schema

- Python의 Dict Type 과 유사
- [https://www.flickr.com/photos/xmodulo/26106186415](https://www.flickr.com/photos/xmodulo/26106186415)



### 7.4.3 JSON in Python

- `json` 모듈을 사용하여 손쉽게 파싱 및 저장 가능
- 데이터 저장 및 읽기는 dict type과 상호 호환 가능
- 웹에서 제공하는 API는 대부분 정보 교환 시 JSON 활용
- 각 사이트마다 Developer API의 활용법을 찾아 사용



### 7.4.4 JSON Read

- JSON 파일의 구조를 확인
- 읽기
- dict type 처럼 처리

```json
{'employees': [
    {'firstName': 'John', 'lastName': 'Doe'},
    {'firstName': 'Anna', 'lastName': 'Smith'},
    {'firstName': 'Peter', 'lastName': 'Jones'}
]}
```

```python
import json

with open('json_example.json', 'r', encoding='utf8') as f:
    contents = f.read()
    json_data = json.loads(contents)
    print(json_data['employees`])
```



### 7.4.5 JSON Write

- Dict type으로 데이터 저장
- json 모듈로 write

```python
import json

dict_data = {'Name': 'Zara', 'Age': 7, 'Class': 'First'}

with open('data.json', 'w') as f:
    json.dump(dict_data, f)
```

