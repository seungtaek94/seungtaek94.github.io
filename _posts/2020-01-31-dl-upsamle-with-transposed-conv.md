---
layout: post
title: '[ML/DL] Transposed Convolution 연산을 이용한 Up-sampling'
subtitle: ''
categories: programing
tags: dl, Convolution, Pytorch, Up-sampling
comments: true
---
 
## Up-Sampling

![](/assets/img/2020-01-31-09-43-27.png){: width="" height=""}*그림 1. Up-sampling이 필요한 경우의 예시*

&nbsp;&nbsp;딥러닝 모델을 생성할때 우리는 저해상도의 레이어에서 고해상도로 Up-sampling이 필요한 경우를 종종 마주친다. 예를 들어 이전 레이어의 출력이 다음과 같을때 `a = [64, 3, 128, 128]`, `b = [64, 256, 32, 32]` 만약 우리가 `dim=1`을 기준으로 Concatenate를 하고 싶다면 우리는 `H, W`를 맞추어 줄 필요가 생긴다. 경우에 따라 `b`를 Up-sampling 하는 레이어를 추가하여 맞추어 줄 수 있다. Up-sampling을 위한 연산으로는 다음의 3가지 이외에도 다양한 방법이 있다.

* Neares neighbor interpolation
* Bi-linear interpolation
* Bi-cubic interpolation

&nbsp;&nbsp;허나 이러한 방법들은 Up-sampling을 하기위해서 보간을 이용한다. 네트워크 설계자가 임의로 파라미터를 설정해줘야하기 때문에 수동적이며 Network는 이를 알 수 없다.

## Transposed Convolution을 이용한 Up-sampling

 &nbsp;&nbsp;`Transposed Convolution` 연산을 이용하면 학습가능한 파라메터로 인하여 보간 방법을 이용하지 않고 Up-sampling이 가능하다.

### Convolution

![](/assets/img/2020-01-31-11-21-36.png){: width="" height=""}*그림 2. Convolution 연산의 예*

&nbsp;&nbsp;위 그림 2.는 간단한 Convolution 연산을 그림으로 나타낸것 이다. 입력 크기는 4x4, kerenl 크기는 3x3, stride=1의 연산을 Padding 없이한 Convlution 연산의 결과는 2x2 출력 크기를 갖는다. 빨간색으로 활성화 된 부분이 연산시 대응되는 부분이다.
&nbsp;&nbsp;Convolution 연산시에 생각해야할 부분은 그림처럼 입력과 출력의 대응되는 부분이 비슷하다는 것이다. 예를 들면 입력의 좌상단의 값은, 출력의 좌상단 부분에 영향을 준다. 또한 예제에서는 입력 9개의 값이 출력 1개을 만들어내는 `many-to-one`의 구조를 갖는다.

Pytorch를 이용해 위의 그림을 코드로 나태내보면 다음과 같다.

```python
x = torch.arange(1, 17, dtype=torch.float32).view(-1, 4)
x = torch.unsqueeze(x, 0)
x = torch.unsqueeze(x, 0)
print(x, x.size())

conv_filter = torch.Tensor([[3, 2, 9], [-2, 1, 3], [-3, -2, 2]])
conv_filter = conv_filter.view(1, 1, 3, 3).repeat(1, 1, 1, 1)
print(conv_filter, conv_filter.size())

out = F.conv2d(x, conv_filter)
print(out)
```

Out:
```
tensor([[[[ 1.,  2.,  3.,  4.],
          [ 5.,  6.,  7.,  8.],
          [ 9., 10., 11., 12.],
          [13., 14., 15., 16.]]]]) torch.Size([1, 1, 4, 4])
tensor([[[[ 3.,  2.,  9.],
          [-2.,  1.,  3.],
          [-3., -2.,  2.]]]]) torch.Size([1, 1, 3, 3])
tensor([[[[26., 39.],
          [78., 91.]]]])
```

### Convolution matrix

![](/assets/img/2020-01-31-11-22-17.png){: width="200" height="200"}*그림 3. 3x3 kernel*

&nbsp;&nbsp;Convolution 연산은 행렬을 이용해 표현할수 있다. 행렬 곱을 위해 위의 3x3 kernel을 4x16 행렬로 나타내면 다음과 같다.

![](/assets/img/2020-01-31-11-32-01.png){: width="" height=""}*그림 4. 4x16 Convolution matrix*

&nbsp;&nbsp; 위의 그림 4.에서 각 열은 그림 2.에서의 각각 4번의 Convolution 연산을 뜻합니다. 행렬 연산을 위해 그림2. 의 입력을 16x1의 벡터로 펴준다.

![](/assets/img/2020-01-31-11-46-19.png){: width="180" height="380"}*그림 5. 입력 matrix 변환*

그 후, 행렬 곱 연산을 하게되면 4x16 * 16x1 하게 되면 출력은 다음 그림 6.과 같이 4x1 행렬이 될것 임을 알수 있다.

![](/assets/img/2020-01-31-11-52-50.png){: width="" height=""}*그림 6. Convolution 연산을 행렬곱으로 나타낸 예시*