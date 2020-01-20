---
layout: post
title: '[ML/DL] Batch Normalization'
subtitle: ''
categories: programing
tags: dl
comments: true
---
## Contents

-   Gradient Vanishing / Exploding
-   Internal Covariate Shift
-   Batch Normalization

## Gradient Exploding

 이전의 Relu 게시글에서 Sigmoid를 사용할 때 발생하는 문제 중 하나로 [Gradient Vanishing](https://blog-st.tistory.com/entry/MLDL-Relu-with-Pytorch) 문제에 대해 설명한적이있다. Exploding의 경우는 Vanishing 문제와는 반대로 Gradient가 너무 커지는 문제를 말한다. 위와 같은 Gradient에 대한 문제를 해결하기 위한 방법으로는 Activation Function을 바꾸거나, Weight Initialization을 잘해주거나 하는 방법이 있고 특별히  Exploding 문제에서는 Learning rate를 작게 해주는 방법이 있다. 이 게시글에서는 이와 같은 간접적인 해결방법이 아닌 Batch Normalization이라는 직접적인 해결방법에 대해 설명한다.

## Internal Covariate Shift

![](/assets/img/2020-01-20-09-08-09.png)*그림 1. Train 및 Test 셋의 분포의 예*

 Batch Normalization의 저자들은 Internal Covariate Shift가 Gradient의 Exploding, Vanishing 문제를 야기한다고 주장한다. Covariate Shift란 위의 그림 1과 같은 분포를 가지는 데이터셋 처럼 우리가 학습에 사용하는 Train 및 Test 셋 간의 분포가 차이를 보인다는 것이다.

![](/assets/img/2020-01-20-09-08-52.png)*그림 2. 학습 데이터에 대한 간단한 레이어의 각 레이어의 분포*

 Internal Covariate Shift란 위의 그림 2. 와 같은 모델이 있을 때 Input과 Output 의 분포에 차이가 있다는 것이다. 즉, 다시 말하면 데이터가 레이어를 거치게 되는데 이때 각 레이어에서 Covariate Shift가 일어나게 되고 이것이 다음 레이어로 전이되면서 결국에는 Output과 Input 데이터의 분포 간의 큰 차이가 생기는 것을 Internal Covariate Shift라고 한다. 따라서, 앞 단의 차이가 뒤로 전이되며 누적됨으로 이문제는 레이어가 깊을수록 크게 나타난다.

## Batch Normalization

> Ioffe, Sergey, and Christian Szegedy. "Batch normalization: Accelerating deep network training by reducing internal covariate shift." arXiv preprint arXiv:1502.03167  (2015).

![](/assets/img/2020-01-20-09-09-25.png){: width="449" height="165"}*그림 3. 간단한 Batch Normalization 예*

 Batch Normalization은 간단하게 설명할 수 있다. 레이어에 서 발생하는 Covariate Shift를 완화하기 위해 모델의 중간 중간에 Normalization을 해주는 레이어를 둔다. 일반적으로 학습을 할 때 Mini-Batch를 사용해 학습을 하기 때문에 이름처럼 각 Mini-Batch마다 Normalization을 해준다.

![](/assets/img/2020-01-20-09-09-48.png){: width="463" height="375"}*그림 4. 논문에 나온 수식을 이용한 설명*

 위의 그림 4. 의 수식을 이용해 더 자세히 설명을 해보자면 각 배치의 평균과 Variance를 계산하고 해당 값을 이용해 Normalization을 해준다. 이때 $$\epsilon$$은 Normalization을 할때 나누는 과정에서 0이 나누어지는 것을 막기 위해 아주 작은 수이다. 이렇게 Normalized 된 결과 $$\hat{x}_i$$에 $$\gamma$$를 곱하고 $$\beta$$를 더해준다. 이 과정이 필요한 이유는 각 Batch마다 계속해서 Normlization을 하게 되면 Activation Function의 Nonlinearity와 같은 성질을 잃게 되기 때문에 $$\gamma$$를 곱하고 Shift($$\beta$$)를 더해주는 과정을 통해 이러한 문제를 완화한다. 이때 $$\gamma$$와 $$\beta$$는 네트워크에 의해 학습되는 Trainable 한 파라미터이다.

>## Reference
> [1] [모두를 위한 딥러닝 시즌2 - PyTorch](https://www.edwith.org/boostcourse-dl-pytorch/joinLectures/22155)