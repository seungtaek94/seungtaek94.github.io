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
```python
x = torch.empty(3, 4)
print(x)
```
Out:
```
tensor([[2.5226e-18, 6.4825e-10, 1.0072e-11, 7.7195e-10],
        [2.6409e-06, 4.0747e-11, 2.6553e-06, 2.9572e-18],
        [6.7333e+22, 1.7591e+22, 1.7184e+25, 4.3222e+27]])
```
> NOTE: `torch.empty()`를 이용해 Tensor를 생성하게 되면 현재 할당된 메모리에 존재하던 값들이 초기값으로 결정된다.  
```
x = torch.rand(3, 4)
print(x)
```
Out:
```
tensor([[0.3018, 0.1164, 0.9890, 0.7646],
        [0.4744, 0.8903, 0.5615, 0.9296],
        [0.5578, 0.2696, 0.5470, 0.1376]])
```
> NOTE: `torch.rand()`를 이용해 랜덤으로 초기화된 Tensor를 생성한다.

---
 ## Permute(dim$$1$$, dim$$2$$, ...,  dim$$n$$)

<span class="code-title">
import torch
</span>