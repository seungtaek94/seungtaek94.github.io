---
layout: post
title: '[Python] List Comprehension'
subtitle: ''
categories: programing
tags: python
comments: true
---

# List Comprehension
- 기존 List를 사용하여 간단히 다른 List를 만드는 기법
- 포괄적인 List, 포함되는 리스트라는 의미로 사용됨
- 파이썬에서 가장 많이 사용되는 기법중 하나
- 일반적으로 for + append 보다 속도가 빠름

<br>

일반 적인 Code:
```python
result = []
for i in range(10):
    result.append(i)
print(result)
```
출력:
```
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

<br>

List Comprehensions 1:
```python
result = [i for i in range(10)]
print(result)

result = [i for i in range(10) if i%2 == 0]
print(result)
```
출력:
```
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
[0, 2, 4, 6, 8]
```

<br>

List Comprehensions 2:
```python
word_1 = "Hello"
word_2 = "World"

result = [i+j for i in word_1 for j in word_2]
print(result)
```
출력:
```
['HW', 'Ho', 'Hr', 'Hl', 'Hd', 'eW', 'eo', 'er', 'el', 'ed', 'lW', 'lo', 'lr', 'll', 'ld', 'lW', 'lo', 'lr', 'll', 'ld', 'oW', 'oo', 'or', 'ol', 'od']
```

<br>

List Comprehensions 3:
```python
case_1 = ['A', 'B', 'C']
case_2 = ['D', 'E', 'A']

result = [i+j for i in case_1 for j in case_2]
print(result)

result = [i+j for i in case_1 for j in case_2 if not (i==j)]
print(result)

result.sort()
print(result)
```
출력:
```
['AD', 'AE', 'AA', 'BD', 'BE', 'BA', 'CD', 'CE', 'CA']
['AD', 'AE', 'BD', 'BE', 'BA', 'CD', 'CE', 'CA']
['AD', 'AE', 'BA', 'BD', 'BE', 'CA', 'CD', 'CE']
```

<br>

List Comprehensions 4:
```python
words = 'The quick brown fox jumps over the lazy dog'.split()
print(words)
print()

stuff = [[w.upper(), w.lower(), len(w)] for w in words]

for i in stuff:
    print(i)
```
출력:
```
['The', 'quick', 'brown', 'fox', 'jumps', 'over', 'the', 'lazy', 'dog']

['THE', 'the', 3]
['QUICK', 'quick', 5]
['BROWN', 'brown', 5]
['FOX', 'fox', 3]
['JUMPS', 'jumps', 5]
['OVER', 'over', 4]
['THE', 'the', 3]
['LAZY', 'lazy', 4]
['DOG', 'dog', 3]
```

<br>

## Reference
> [머신러닝을 위한 Python](https://www.edwith.org/aipython/lecture/22953/)