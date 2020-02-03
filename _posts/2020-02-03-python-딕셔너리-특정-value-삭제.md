---
layout: post
title: '[Python] 딕셔너리(Dictionary) 특정 Value를 가진 요소 삭제'
subtitle: ''
categories: programing
tags: python
comments: true
---

 알고 리즘 문제를 풀다 Dictionary에서 특정 Value를 가진 요소를 삭제할 필요가 있었다.

Code:
```python
x = {'a':1, 'b':2, 'c':3, 'd':4}
b = x
for key, value in b.items():
    if value == 3:
        x.pop(key)
print(x)
```
Out:
```
RuntimeError: dictionary changed size during iteration
```
<br>

&nbsp;&nbsp;삭제를 위해 반복문을 사용했는데, 만약 `x.items()`를 이용해 반복문을 돌리고 안에서 `x`의 value를 삭제하면 박복문에 영향이 있을것 같아서 `x`를 `b`에 복사 하고 `b.items()`로 반복문을 돌리고 `x`에서 요소를 제거 하려고 생각했는데 에러가 발생했다. 찾아보니 반복문 안에서는 어떠한 Dictonary의 size에 영향이 가는 코드를 작성하면 안되는 것 같다.

&nbsp;&nbsp;해결 방법은 다음과 같다. 반복문 안에서 특정 값을 제거하는 것이 아닌, 새로운 Dictionary를 선언하고 그 안에 특정 Value를 제외하고 넣으면 된다.

Code:
```python
x = {'a':1, 'b':2, 'c':3, 'd':4}
b = {}
for key, value in x.items():
    if value != 3:
        b[key] = value
print(b)
```
Out:
```
{'a': 1, 'b': 2, 'd': 4}
```
> Note: Dictionary `x`에서 value가 3인 요소를 삭제하고 싶을때.

<br>

아래는 같은 결과를 가진 좀더 짧은 코드 이다.

Code:
```python
x = {'a':1, 'b':2, 'c':3, 'd':4}
x = {key: value for key, value in x.items() if value != 3}
print(x)
```
Out:
```
{'a': 1, 'b': 2, 'd': 4}
```