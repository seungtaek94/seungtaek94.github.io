---
layout: post
title: '[Python] f-string 포매팅'
subtitle: ''
categories: programing
tags: python
comments: true
---

# f-string 포매팅
> NOTE: `f-string` 포매팅은 파이썬 `3.6` 버전부터 사용할 수 있다.

&nbsp;&nbsp;`f-string`은 문자열 앞에 `f`를 접두어로 붙이고 `{표현식(expression)}`을 사용하여 표현식의 값을 삽입해 사용할 수 있다.다음의 코드를 보면 이해하기 쉽다.

```python
day = '화'
Y = '2020'
M = '2'
D ='11'

print(f'오늘은 {Y}년 {M}월 {D}일 {day}요일 입니다.')
```

출력:
```
오늘은 2020년 2월 11일 화요일 입니다.
```
---

문자열 `정렬`은 다음과 같이 할 수 있다.

```python
print(f'|{"Hellow World!!":<30}|') # 왼쪽 정렬
print(f'|{"Hellow World!!":>30}|') # 오른쪽 정렬
print(f'|{"Hellow World!!":^30}|') # 가운데 정렬
```

출력:
```
|Hellow World!!                |
|                Hellow World!!|
|        Hellow World!!        |​
```

---

다음과 같이 특정 문자로 `공백`을 채울 수 있다.
```python
print(f'|{"Hellow World!!":*<30}|') # 왼쪽 정렬하고 공백을 '*'로 채움
print(f'|{"Hellow World!!":@>30}|') # 오른쪽 정렬하고 공백을 '@'로 채움
print(f'|{"Hellow World!!":0^30}|') # 가운데 정렬하고 공백을 '0'로 채움
```

출력:
```
|Hellow World!!****************|
|@@@@@@@@@@@@@@@@Hellow World!!|
|00000000Hellow World!!00000000|
```

---

자릿수의 표현
```python
import math

print(f'|{math.pi:.2f}|')
print(f'|{math.pi:.3f}|')
print(f'|{math.pi:.10f}|')
print(f'|{math.pi:0>12.2f}|')
print(f'|{math.pi:0<12.2f}|')
```

출력:
```
|3.14|
|3.142|
|3.1415926536|
|000000003.14|
|3.1400000000|
```