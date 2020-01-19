---
layout: post
title: '[ML/DL] Convoltution'
subtitle: ''
categories: programing
tags: dl
comments: true
---

## Convolution 

![](/assets/img/2020-01-20-08-16-44.png){: width="728" height="313"}*그림 1. Convolution 연산의 예*

 CNN(Convolution Neural Network)에 들어가기 앞서 Convolution이 무엇인지에 대해 알아본다. Convolution 연산이란 쉽게 설명하자면, 이미지 혹은 행렬 등에서 stride 값만큼 filter(kernel)을 이동시키면서 겹치는 부분의 각 원소의 값을 곱해 모두 더한 값을 출력으로 하는 연산이다. 정확한 연산 방법과 출력은 위의 그림 1. 과 같다.

## Stride

![](/assets/img/2020-01-20-08-18-04.png)*그림 2. Stride*

 그림 2. 는 Stride에 대한 이해를 돕기 위한 그림이다. Stride 가 1일 경우 위의 그림처럼 Filter는 한 칸을 움직이고 다시 Convolution 연산을 하게 된다. Stride 가 2일 경우는  Filter는 2칸을 이동한다. Stride는 Output의 크기에 영향을 미친다. 위의 그림과 같은 경우에는 Stride가 1 일 때 Output 사이즈는 3x3이지만  Stride가 2일 때 Output 사이즈는 2x2가 된다.

## Padding

![](/assets/img/2020-01-20-08-18-45.png){: width="321" height="336"}*그림 3. Padding*

 위의 그림 1. 이나 그림 2.처럼 Filter 혹은 Stride에 따라 Output 사이즈가 Input과 달라지는 것을 막거나 원하는 Output 사이즈를 만들고 싶다면 위의 그림 3.처럼 Input 데이터에 Zero-padding을 추가하여 Convolution 연산을 하면 된다. 

## Output Size

$$ Output Size = {input size - filter size + (2*padding) \over Stride} + 1 $$

Convolution 연산에 의한 Output의 크기는 위의 공식을 통해 계산할 수 있다. 

>## Reference
> [1] [모두를 위한 딥러닝 시즌2 - PyTorch](https://www.edwith.org/boostcourse-dl-pytorch/joinLectures/22155)