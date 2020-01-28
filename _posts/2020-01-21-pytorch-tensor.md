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
<br>

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

> NOTE: `torch.zeros()`를 이용해 0 초기화된 Tensor를 생성한다.

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

<div class="code-title">
    x.size()
</div>

> NOTE: Tensor x의 크기를 반환한다.

Example:
```python
x = torch.zeros(3, 4)
print(x.size())
```
Out:
```
torch.Size([3, 4])
```
<br>

---

## Tensor의 연산(Operations)

<div class="code-title">
    torch.add(input, other, out=None)
</div>

> NOTE: 입력받은 두 Tensor의 덧셈 결과를 반환한다.  
> $$ out = input + ohter $$

Example1 :
```python
x = torch.rand(3, 4)
y = torch.rand(3, 4)
print(torch.add(x, y)) # print(x + y)와 같이도 사용가능하다.

torch.add(x, y, out=result)
print(result)
```
Out1 :
```
tensor([[1.1332, 0.6195, 1.2721, 0.5993],
        [1.1074, 0.8709, 0.4900, 0.5190],
        [0.3774, 1.1385, 0.8968, 1.0966]])

tensor([[1.1332, 0.6195, 1.2721, 0.5993],
        [1.1074, 0.8709, 0.4900, 0.5190],
        [0.3774, 1.1385, 0.8968, 1.0966]])
```
<br>

> In-Place 방식의 Tensor 연산은 `_`를 접미사로 이용한다. ex) `x.mul_(y)`, `x.copy_(y)`등의 연산은 `x`를 변경한다.

Example2 :
```python
y.add_(x)
print(y)
```
Out2 :
```
tensor([[1.1332, 0.6195, 1.2721, 0.5993],
        [1.1074, 0.8709, 0.4900, 0.5190],
        [0.3774, 1.1385, 0.8968, 1.0966]])
```
<br>

* numpy와 같은 인덱싱 표기 방법을 사용할 수도 있다.

Example2 :
```python
x = torch.rand(3, 4)

print(x)
print(x[:1])
print(x[:2])
print(x[0])
print(x[:,1])
```
Out2 :
```
tensor([[0.7823, 0.7104, 0.3771, 0.9301],
        [0.5061, 0.4137, 0.5294, 0.3481],
        [0.7118, 0.1176, 0.8117, 0.7765]])
        
tensor([[0.7823, 0.7104, 0.3771, 0.9301]])

tensor([[0.7823, 0.7104, 0.3771, 0.9301],
        [0.5061, 0.4137, 0.5294, 0.3481]])

tensor([0.7823, 0.7104, 0.3771, 0.9301])

tensor([0.7104, 0.4137, 0.1176])
```
<br>

<div class="code-title">
    torch.view()
</div>

> NOTE: `torch.view`는 Tensor의 size혹은 shape을 변경할때 사용한다.  
> `-1`이 인자로 주어지는 경우 다른 주어진 차원으로 부터 해당 차원을 유추한다.  

Example :
```python
x =torch.randn(4, 4)
y = x.view(16)
z = x.view(-1, 16)
w = x.view(-1, 4)

print(x.size(), y.size(), z.size(), w.size())
```
Out :
```
torch.Size([4, 4]) torch.Size([16]) torch.Size([1, 16]) torch.Size([4, 4])
```
<br>

---
# 작성중....

<div class="code-title">
    func
</div>

> NOTE: 

Example :
```python
code
```
Out :
```
output
```