---
layout: post
title: '[PR] Improved training of binary networks for human pose estimation and image
recognition'
subtitle: ''
categories: pr
comments: true
---
> ## Improved training of binary networks for human pose estimation and image recognition
>
> Bulat, Adrian, et al. "Improved training of binary networks for human pose estimation and image recognition." arXiv preprint arXiv:1904.05868 (2019).

## Abstract

&nbsp;&nbsp;큰 데이터 세트에 대해 대규모 신경망은 다양한 문제의 성능을 크게 향상 시켰다. 그러나 메모리가 부족하고 계산 능력이 제한적일 경우 정확도가 상당히 떨어진다. 본 논문에서 저자들은 이진화 된 신경망(Binarized Neural Networks, 특징(Feautres)과 가중치(Weights)가 모두 이진인 네트워크)의 정확도를 크게 향상 시키는 일련의 방법(테크닉) 제안한다. 저자들은 Human pose estimation과 대규모 이미지 인식(ImageNet classification)을 수행하여 저자들의 방법에 대한 평가를 진행했다.

저자들은 다음과 일련의 새로운 방법론적 변화를 소개한다.

- (a) 보다 적절한 Activation functions
- (b) 역순 초기화(reverse order initialization)
- (c) 점진적인 양자화(progressice quantization)
- (d) 네트워크 stacking

&nbsp;&nbsp;이러한 방법의 추가로 기존의 최신 네트워크의 이진화 기술이 크게 향상됨을 확인 할 수 있다. 저자들은 Human-Pose-Estimation 데이터셋 MPII에 대한 제안된 방법의 성능평가 에서 4%이상의 성능 향상, ImageNet Classification에서는 오류율이 4% 감소함을 확인했다.

### Network Quantization(네트워크 양자화)

&nbsp;&nbsp;Network Quantization이란 신경망의 가중치(Weights) 혹은 특징(Features)를 양자화 하는것을 의미한다. 네트워크 양자화는 모델의 압축 및 효율적인 모델 추론의 한 방법으로서 매우 활발한 연구 주제 중 하나이다. 관련된 선행연구 [1]에서는 가중치화 특징의 이진화에 초점을 둔다. 이것은 {-1, 1}로 양자화 하는것을 목표로한다. 이러한 연구는 최대 압축 및 속도 향상을 기대 할 수 있다.

### Knowledge Distillation

&nbsp;&nbsp;선행 연구 [2]에서는 다른 네트워크의 Knowledge를 distillation 함으로써 소규모 네트워크의 성능을 향상시킬 수 있는 것을 확인했다. Knowlege distillation에서 한 CNN은 "Teacher" 다른 것은 "Student"라 부른다. 일반적으로 "Teacher"은 정확도가 높은 대용량 모델이며 "Student"는 훨씬 컴팩트한 모델로 계산량이 훨씬 작다. Knowlege distillation의 목표는 "Teacher"모델을 이용하여 "Student"모델의 정확도가 "Teacher" 모델의 정확도에 근접할 수 있도록 학습하는 것이다.

&nbsp;&nbsp;대부분의 선행 영구에서는 신경망의 real-valued를 distilling하는데 중점을 두었다. 그러나 이진화 신경망에 대한 그러한 접근 방법은 전혀 효과가 없었다. 본 논문의 저자들은 이러한 "Knowledge Distilation" 기법을 이진 네트워크에 적용하여 정확도 향상에 긍정적인 효과를 가질 수 있다는 것을 실험적으 증명하였다.

### Human Pose Estimation

&nbsp;&nbsp;최근 많은 Human pose estimation과 관련한 많은 연구가 제안되었다. 저자들은 낮은 메모리에서의 효율적인 추론이 아니라 모델의 정확성에 초점을 맞추었다. 본 논문의 저자들은 효율성을 높이는 동시에 가능한 한 높은 정확도를 유지하도록 하였으며 Hourglass(HG) 구조를 사용하엿지만 모든 부분에서 다르게 만드는데에 중점을 두었다.

## 방법

 자성중..

## 결과

 contents

## Reference
>[1]&nbsp;M. Courbariaux, Y. Bengio, and J.-P. David. Binaryconnect:
Training deep neural networks with binary weights during
propagations. In NIPS, 2015
>
>[2]&nbsp;G. Hinton, O. Vinyals, and J. Dean. Distilling the knowledge in a neural network. arXiv preprint arXiv:1503.02531, 2015.