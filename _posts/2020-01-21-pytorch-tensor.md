---
layout: post
title: '[Pytorch] Tensor'
subtitle: 'tensor, pytorch'
categories: programing
tags: pytorch
comments: true
---

# Tensor

&nbsp;&nbsp;텐서는 다차원 배열을 처리기위한 Pytorh의 가장 기본이 되는 데이터형이다. 잘 알려진  *Numpy*의 ndarray와 비슷하며 CPU 및 GPU를 이용한 계산이 가능하다.

 
## Tensor의 생성 방법
<div class="code-title">
    torch.empty()
</div>

> NOTE: `torch.empty()`를 이용해 Tensor를 생성하게 되면 현재 할당된 메모리에 존재하던 값들이 초기값으로 결정된다.

Example 1:
```python
# 3x4 크기의의 Tensor 생성
x = torch.empty(3, 4)
print(x)
```
Out 1:
```
tensor([[2.5226e-18, 6.4825e-10, 1.0072e-11, 7.7195e-10],
        [2.6409e-06, 4.0747e-11, 2.6553e-06, 2.9572e-18],
        [6.7333e+22, 1.7591e+22, 1.7184e+25, 4.3222e+27]])
```

Example 2:
```python
# 임의의 값을 직접 넣어 Tensor 생성
x = torch.tensor([5, 5, 3, 3])
print(x)
```
Out 2:
```
tensor([5, 5, 3, 3])
```
<br>

<div class="code-title">
    torch.rand()
</div>

> NOTE: `torch.rand()`를 이용해 랜덤으로 초기화된 Tensor를 생성한다.

Example:
```python
x = torch.rand(3, 4)
print(x)
```
Out:
```
tensor([[0.3018, 0.1164, 0.9890, 0.7646],
        [0.4744, 0.8903, 0.5615, 0.9296],
        [0.5578, 0.2696, 0.5470, 0.1376]])
```
<br>

<div class="code-title">
    torch.zeros()
</div>

> NOTE: `torch.zero()`를 이용해 0 초기화된 Tensor를 생성한다.

Example:
```python
# 3x4 크기의 0으로 최기화된 long 타입의 Tensor 생성
x = torch.zeros(3, 4, dtype=torch.long)
print(x)
```
Out:
```
tensor([[0, 0, 0, 0],
        [0, 0, 0, 0],
        [0, 0, 0, 0]])
```
<br>
---

## Permute(dim$$1$$, dim$$2$$, ...,  dim$$n$$)

<div class="code-title">
import torch
</div>

---
# 작성중....