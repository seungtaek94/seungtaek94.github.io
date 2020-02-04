---
layout: post
title: '[Python] String(문자열) 관련'
subtitle: ''
categories: programing
tags: python
comments: true
---

## String 관련 함수 정리
### uppser()
<div class="code-title">
    str.upper()
</div>

> NOTE: `str.upper()` 함수를 이용하여 문자열을 대문자로 변환할 수 있다.

Example:
```python
x = 'asdAAAd'.upper()
print(x)
```
Out :
```
ASDAAAD
```
<br>

### lower()
<div class="code-title">
    str.lower()
</div>

> NOTE: `str.lower()` 함수를 이용하여 문자열을 소문자로 변환할 수 있다.

Example:
```python
x = 'asdAAAd'.lower()
print(x)
```
Out :
```
asdaaad
```
<br>

### replace()
<div class="code-title">
    str.replace(old, new, [count])
</div>

> NOTE: `str.replace()`는 특정 문자(`old`)를 새로운 문자(`new`)로 치환 합니다. 만약 `count` 값이 주어 진다면, 앞에서부터 `count` 횟 수 만큼만 치환 합니다. 

Example:
```python
x = 'abc,def,ghi,jkl'

test1 = x.replace(',', '-')
test2 = x.replace(',', '-', 2)
test3 = x.replace(',', '-', 1)

print(test1)
print(test2)
print(test3)
```
Out :
```
outputabc-def-ghi-jkl
abc-def-ghi,jkl
abc-def,ghi,jkl
```
<br>

---
### 작성중
<div class="code-title">
    func
</div>

> NOTE: 

Example:
```python
code
```
Out :
```
output
```
<br>