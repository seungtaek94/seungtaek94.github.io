---
layout: post
title: '[PR] Simple Baselines for Human Pose Estimation and Tracking'
subtitle: ''
categories: pr
#tags: deeplearning
comments: true
---
# Paper

**Simple Baselines for Human Pose Estimation Tracking**

> Xiao, Bin, Haiping Wu, and Yichen Wei. "Simple baselines for human pose estimation and tracking."_Proceedings of the European Conference on Computer Vision (ECCV)_. 2018.

## 문제 정의

 최근  몇년간 Human Pose Estimation 분야는  상당히 발전하고 관심 또한 높아졌다. 동시에 전체 적인 알고리즘 및 시스템의 복잡도 또한 증가했다. 그에 따라 알고리즘을 만들고 분석하고 비교하는것이 더 어려워졌다. 이 논문에서는 간단하고 효과 적인 Baseline 방법을 제안하며 해당분야에 대한 새로운 아이디어를 고무시키고 평가하는 데 도움을 준다.

## 방법

![](/assets/img/2020-01-17-16-43-56.png)*그림1. Pose Estimation을 위한 기존 네트워크 및 본 논문에서 제안한 (c) Simple Baseline 네트워크*

 본 논문에서는 ResNet의 마지막 Convolution layer에 \*Deconvolution layer(논문에서는 $$C_5$$라 함)을 추가한 아주 간단한 형태의 네트워크를 제안한다. 본 논문에서 제안한 네트워크의 구조는 그림1.의 (c)와 같다. 기본적으로 네트워크는 3개의 Deconvolution Layer가 존재하며 각각의 Layer는 Batch Normalization과 Relu를 이용한다. 또한 각 Layer는 256 Filters, 4x4 kernel(Stride=2)의 형태를 가지며 마지막 레이어의 끝에서 1x1 Convolution연산을 통해  $$k$$개의 Keypoints를 위한 예측된  Heatmap $${H_1,...,H_k}$$를 생성한다. loss 함수로는 Mean Squared Error(MSE)를 사용한다.

 저자들이 이러한 구조를 갖는 네트워크를 설계한 이유는 다음과 같다. 이러한 구조를 선택한 이유는 깊은 저-해상도의 Feauture로부터 Heatmap을 생성하기 가장 간단한 구조이며 SOTA 네트워크인 Mask-RCNN에서도 적용된 방법이다.

  다른 기존의 방법(그림1. (a), (b))은 Feature Map의 Resolution을 높이기 위해 Upsampling을 이용하고 다른 Block에 Convolution Parameter를 연결한다. 그와 다르게 본 논문에서는 Upsampling과 Convolution Parameter를 Deconvolution Layer 안에 합쳤다. 따라서  Skip Connection을 이용하는 다른 기존의 방법에 비해 High Resolution Feature Map을 생성하는 방법이 명료하다.

 본 네트워크와 기존의 다른 방법들과의 공통점은 High resolution Feauture Map과 Heatmap을 얻기 위하여 3단계의 Upsampling과 3단계의 비-선형성을 이용한다. 이러한 관찰을 통해, "_High resolution Feautre Map을 얻는 것은 중요하나, 어떻게 얻는지는 상관 없다"_는 사실을 알 수있다(간단하면 간단할수록 이득이다).

 \*Deconvolution Layer: 이 논문에서 저자들은 Deconvolution이라는 용어를 사용하고 있지만 실제 일어나는 연산은 Transposed Convolution 연산이다. [이곳](https://datascience.stackexchange.com/questions/6107/what-are-deconvolutional-layers)에서 정확한 설명과 이유를 알 수 있다.

## 결과

![](/assets/img/2020-01-17-16-46-52.png){: width="728" height="294"}*그림 2. COCO 2017 val2017  dataset에 대한 결과*

 위 그림 2. 는 COCO 2017 validation set에 대한 실험결과이다. 위의 실험을 통해 정확도에 가장 큰 영향을 미치는 변수는 입력 이미지의 크기 임을 알수 있고, Deconvoltuion 레이어의 Kernel 크기는 큰것이 좋으나 차이는 미비 함을 알 수 있다. 당연하게도 좀더 깊은 레이어를 가진 Backbone 네트워크를 사용했을때 유리하며 Deoconvolution 레이어의 깊이 또한 깊을 수록 정확도도 높아짐을 알 수 있다.