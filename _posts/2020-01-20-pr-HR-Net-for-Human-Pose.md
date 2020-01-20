---
layout: post
title: '[PR] Deep High-Resolution Representation for Human Pose Estimation'
subtitle: ''
categories: pr
comments: true
---
> ## **Deep High-Resolution Representation for Human Pose Estimation**
>
> Sun, Ke, et al. "Deep high-resolution representation learning for human pose estimation." arXiv preprint arXiv:1902.09212 (2019).

## 문제 정의
 ![](/assets/img/2020-01-20-09-33-37.png)*그림 1. 기존 방식의 예(LeNet-5)*

 본 논문에서는 신뢰할 수 있는 고해상도 표현(Represntations)의 학습에 주목한다. 기존의 대부분의 연구들에서는 고해상도 표현을 학습하기위해 그림 1.과 비슷한 구조의 고에서 저 해상도의 Convolution 층을 직렬로 연결한 네트워크(High-to-Low Resolution network)를 사용해 저해상도 표현을 고해상도 표현으로 복구 하는 방법을 이용한다. 본 논문에서 저자들은 <span style="color:red"><I>고해상도 표현을 전체 과정에서 유지하는 네트워크</I></span>를 제안한다. 

## 방법

![](/assets/img/2020-01-20-09-40-47.png)*그림 2. 기존 Classification Network 구조*
   
 다시 한번 이전의 네트워크의 구조를 보면 그림2.와 같다. 여러 해상도를 가진 Convolution Layer를 <span style="color:skyblue"><I>직렬(Series)</I></Span>로 연결한 형태를 갖는다. 그러나 이러한 방식은 저해상도의 표현을 이용해 고해상도 표현을 얻게 되는데 이과정에서 일련의 손실이 일어난다. 

![](/assets/img/2020-01-20-09-46-37.png)*그림 3. 저자들이 제안한 병렬(Parallel) 연결 방식*

 저자들은 위에서 말한 문제를 해결하기 위하여 여러 해상도의 네트워크들을 <span style="color:blue"><I>병렬(Parallel)</I></span>로 연결하는 방법을 제안한다. 위와 같은 구조를 이용하여 네트워크 전체 과정에서 고해상도 표현을 유지할 수 있다.

 ![](/assets/img/2020-01-20-10-03-07.png)
 *그림 4. 저자들이 제안한 Repeated Fusions*
 ![](/assets/img/2020-01-20-10-08-49.png)
 *그림 5. Repeated Fusions의 세부 구조*
 *Down-sample: stride-2, 3x3*
 *Up-sample: bilinear, 1x1*

 기존의 U-Net, Hour-Glass와 같은 네트워크에서는 다해상도 표현은 결합하기 위해 Skip Connection을 이용하 였지만 본논문에서 저자들은 여러 다해상도의 표현을 Fusion해 네트워크의 출력 Heatmap을 얻기 위해 저자들은 그림 4., 그림 5.와 같은 구조의 <span style="color:red"><I>Repeated Fusions</I></span>을 제안한다. 이러한 구조는 고해상도 표현을 유지하고 네트워크의 파라미터 수를 줄이는데에 도움을 준다.
 
## 결과

 ![](/assets/img/contents.png){: width="" height=""}*그림 6. COCO keypoints 데이터셋에 대한 실험결과*

 위 그림 6.은 COCO 데이터셋에 대한 저자들의 제안한 방법의 실험 결과이다. 기존의 방법에 비해 정확도가 높음을 알수 있고, 비슷한 정확도의 기존의 다른 방법들에 비하여 파라미터 수가 적음을 통해 저자들이 제안한 구조가 효율적임을 알 수 있다.

 현재 본 네트워크는 Pose Estimation 뿐만아니라 다른 도메인들(Image Classification, Object Detection, Semantic Segmentation, Face alignment)에서도 SOTA 결과를 달생했다.