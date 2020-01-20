---
layout: post
title: '[ML/DL] Weight Initialization'
subtitle: ''
categories: programing
tags: dl
comments: true
---


## 왜 Weight Initailization을 잘하는것이 중요한가?

>![](/assets/img/2020-01-20-15-22-12.png){: width="552" height="380"}*Understanding the difficulty of training deep feedforward neural networks."&nbsp; Proceedings of the thirteenth international conference on artificial intelligence and statistics . 2010.*

&nbsp;&nbsp;위의 그림에서 **"N"**이 붙은것이 어떠한 Weight Initialization 을 진행한것이고 그렇지않은 것이 기존의 방식처럼 랜덤하게 Weight Initialization을 한것이다. 랜덤한것보다 다른 방법이 더 좋은 성능을 보임을 확인할 수 있다. 우리는 이러한 결과를 토대로 Weight Initialization을 잘 하는것이 딥러닝의 성능에 큰 영향을 미침을 확인할 수 있다.

## Restricted Boltzmann Machine(RBM)

![](/assets/img/2020-01-20-15-23-39.png){: width="" height=""}*[RBM](https://en.wikipedia.org/wiki/File:Restricted-boltzmann-machine.svg)*

&nbsp;&nbsp;RBM에서 Restricted는 같은 Layer 안의 노드들 끼리는 서로 연결이 없다는 것을 의미한다. 이와같이 Layer 안에서는 연결이 없고 다른 Layer 와는 Fully Connected한 형태를 RBM이라한다. 아래에서는 RBM을 이용해 어떻게 Weigt을 초기화 하였는지 알아본다.

## Deep Belief Network

> Larochelle, Hugo, et al. "An empirical evaluation of deep architectures on problems with many factors of variation."_Proceedings of the 24th international conference on Machine learning_. ACM, 2007.

![](/assets/img/2020-01-20-15-25-32.png){: width="478" height="229"}*Pre-training*

&nbsp;&nbsp;Deep Belief Network에서는 위와 같은 방식으로 RBM을 이용해 Weight을 초기화 시킨다. 먼저 첫번째 스탭 (a) 두개의 Layer에 대해 RBM으로 학습을한다. 다음 스탭 (b) 에서는 레이어를 하나 추가하고 (a)에서 학습된 레이어의 Weight을 Fix하고 추가한 레이어에 대해 RBM 학습을한다. 이러한 단계를 반복적으로 마지막 레이어까지 계속해서 반복한다. 이러한 과정을 **Pre-training** 이라고 한다.


![](/assets/img/2020-01-20-15-26-19.png){: width="196" height="269"}*Fine-tuning*


&nbsp;&nbsp;이후 RBM 으로 Pre-Training이된 네트워크를 우리가 일반적으로 사용하는 학습방법인, 입력 X에 대한 예측 Y를 구하고 Ground-Truth(GT)와의 차이를 구해 Backpropagation을 통한 네트워크를 업데이트를 하는데 이단계를 **Fine-Tuning** 이라한다. 그러나 지금은 이러한 RBM을 이용한 Weight Initialization 방법을 거의 사용하지 않는다. 현재는 아래의 Xavier와 He Initialization 방법을 많이쓴다. 각각의 매우 간단한 수식을 이용해 Weight을 초기화를 함에도 불고하고 괸장히 좋은 성능을 보여준다.

## Xavier initialization

-   Xavier Normal initialization

$$ W \backsim N(0,Var(W)) $$

$$ Var(W) = \sqrt{2 \over {n\_{in}+n\_{out}}}$$

-   Xavier Uniform initialization

$$W \backsim U(-\sqrt{6 \over {n\_{in}+n\_{out}}}, +\sqrt{6 \over {n\_{in}+n\_{out}}})$$

## He Initialization

-   He Normal initialization

$$W \backsim N(0,Var(W))$$

$$Var(W) = \sqrt{2 \over n\_{in}}$$

-   He Uniform initialization

$$ W \backsim U (-\sqrt{6 \over {n\_{in}}}, + \sqrt{6 \over {n\_{in}}})$$

\*$$n\_{in}$$: Layer의 Input 수, $$n\_{out}$$: Layer의 Output 수

>## Reference
> [1] [모두를 위한 딥러닝 시즌2 - PyTorch](https://www.edwith.org/boostcourse-dl-pytorch/joinLectures/22155)