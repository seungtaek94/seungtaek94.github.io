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

![](/assets/img/2020-02-14-08-58-21.png){: width="" height=""}*그림 1. 이진화된 CNN을 위해 설계된 Residual blocks*

### Baseline

&nbsp;&nbsp;저자들은 [3]의 구조를 저자들의 제안 방법의 개선에 대한 Baseline으로서 사용하였다. [3]은 HourGlass 구조과 이진 CNN을 위한 새로 설계된 잔차 블록(Residual block)을 결합한다(그림 1.). 네트워크는 다음과 같이 [4]에 설명된 접근 방식을 사용해 이진화되었다:

 $$ T\ *\ W  \approx (sgn(T) \circledast sgn(W))K\alpha $$

$$T$$는 입력 tensor, $$W$$는 레이어들의 가중치 tensor,  $$K$$는 모든 sub-tensor $$T$$에 대한 scaling factor를 포함 하는 행렬, $$\alpha \in \mathbb{R}^+$$는 가중치를 위한 scaling factor이다. $$\circledast$$는 비트 단위(bitwise) XNOR로 효율적으로 구현된 이진화된 컨볼루션 연산을 나타내며 약 58배의 속도 향상과 약 32배의 모델 압축 비율을 제공한다. 실제로는 $$K$$를 사용하지 않는다(무시할만한 성능 저하로 네트워크의 속도를 높힌다).

### Leaky non-linearities

&nbsp;&nbsp;선행 연구 [3, 4]에서는 각 컨보루션 레이어 뒤에 비선형 성을 추가하는 것이 이진화된 CNN의 성능을 향상시키는 데 사용될 수 있음 보여 주었다. 저자들은 비선형 성의 선택과 이전에 제안된 ReLU의 부정적인 영향을 경험적으로 보여주는 Human pose estimation에 대한 전반적이 성능에 대해 엄격히 탐구한다. ReLU를 사용하는 대신 최근에 소개된 PReLU를 적용하여 ReLU 및 Leaky ReLU 보다 성능이 우수하다는 것을 보여준다.

![](/assets/img/2020-02-14-10-33-56.png){: width="" height=""}*그림 2. MPII 데이터셋에 대한 훈련중 정확도 평가*

&nbsp;&nbsp;저자들이 제안한 방법에는 두가지 전제 조건이 있다. 우선 $$sgn$$ 함수를 이용하여 filter 및 features가 나타낼수 잇는 상태를 {-1, 1}로 제한한다(이진화 과정).
따라서, 네트워크의 표현은이 두 가지 상태에 있으며, 각 컨볼루션 레이어마다 ReLU를 사용하여 훈련하는 동안  이들 중 하나를 제거하면 불안정해 진다. (그림 2. 참조) 두번째로 이 불안정성은 부호 함수의 구현이 0에서 "Leaky(누설)"되어 원치 않는 불완전한 상태를 야기하고 다음의 반복에서 두 상태 사이에서 쉽게 건너 뛸 수 있는 사실로 인해 더욱 증폭된다. 그림

![](/assets/img/2020-02-14-11-55-01.png){: width="" height=""}*그림 3. 네트워크 진행에 따른(왼쪽에서 오른쪽 그림) PReLU(첫번째 행) 및 ReLU(두 번째 행)을 사용한 계층에 대한 가중치 분포

&nbsp;&nbsp;위의 그림3.에서 보여 주듯이 ReLU는 네트워크가 진행함에 따라 가중치를 0에 더 깝갑게 하기 때문에 상태간의 점프 가능성을 높이며 불안정성을 띈다. 반면에, PReLU는 네트워크가 진행 함에도 불구하고 안정적인 분포를 보인다. 따라서 저자들은 PReLU의 사용이 네트워크의 표현력을 높이는 효과를 가지며 위에서 언급한 불안정성을 제거할수 있다고 결론지엇다.

### Reverse-order initialization

&nbsp;&nbsp;신경망의 좋은 성능 달성을 위해서는 적절한 초기화가 필요하다. 양자화된 네트워크에 대해서도 마찬가지다. 선행 연구들에서는 사전 훈련된 신경망을 이용해 초기화 한다. 그런나 sgn의 출력신호는 ReLU 계층의 출력과 매우 다름으로 이러한 방법을 사용하면 치명정인 정확도 손실이 발생한다.

![](/assets/img/2020-02-14-15-34-39.png){: width="" height=""}*그림 4.  서로다른 최기화 방법을 사용한 모델의 MPII 데이터 셋의 학습하는 동안의 정확도*

&nbsp;&nbsp;이를 완화하기 위해 저자들은 현재 실제값(real-valued)에서 이진 네트워크를 초기화 하는 표준 방법과는 반대되는 방법을 제안한다. 먼저 real weight과 이진 특징으로 네트워크를 학습하는 것이 좋다. 그리고 이후에 가중치를 이진화 하도록 한다. 이렇게 함으로써 문제를 효과적으로 두가지 하위 문제로 나눌수 있다: 가중치화 특징 이진화는 가장 어려운 것부터 쉬운것까지 해결하려 한다(?). 그림 4.는 기존의 사전 훈련방법에 대한 제안된 초기화 방법의 이점을 확인 시켜준다.

### Smooth Progressive Quantization

&nbsp;&nbsp;선행 연구에서는 정밀도를 점차적으로 감소 시키거나 양자화된 가중치의 양을 분할하고 점진적으로 증가시키는 것이(네트워크를 점진적으로 양자화) 적절한 성능 향상을 가져온다는 것을 보여 주었다.

&nbsp;&nbsp;대신 이 연구에서 저자는 추정 오차가 $$\lambda$$에 의해 제어되는 것이 아니라 $$sgn(x)$$을 근사화 하도록 하는 다른 방법을 따른다. 이는 학습과정중에 점차적으로 증가 함으로써 점진적인 이진화를 달성한다. 이것은 이진화가 될 가중치의 선택이 암시적으로 발생하는 자연스럽고 부드러운 전이를 야기하고 양자화된 가중치의 양을 증가시키기 위해 고정된 스케쥴링을 정의할 필요 없이 람다를 변화 시킴으로써 쉽게 제어할 수 있다.
 
&nbsp;&nbsp;다음은 $$sgn(x)$$ 에 근사하기 위한 몇가지 옵션입니다:
#### Sigmoid:

$$ sgn(x) \approx 2\left(e^{\lambda x} \over {1+e^{\lambda x}} \right)-1 $$

$$ {d \over dx} 2 \left({e^{\lambda x} \over {1+e^{\lambda x}}} \right)-1 = {{2\lambda e^{\lambda x}} \over {\left(e^{\lambda x}+1 \right)^2}} $$

#### SoftSign:

#### Tanh:


## 결과

 contents

## Reference
>[1] M. Courbariaux, Y. Bengio, and J.-P. David. Binaryconnect:
Training deep neural networks with binary weights during
propagations. In NIPS, 2015
>
>[2] G. Hinton, O. Vinyals, and J. Dean. Distilling the knowledge in a neural network. arXiv preprint arXiv:1503.02531, 2015.
>
>[3] A. Bulat and G. Tzimiropoulos. Binarized convolutional
landmark localizers for human pose estimation and face
alignment with limited resources. In ICCV, 2017.
>
>[4] M. Rastegari, V. Ordonez, J. Redmon, and A. Farhadi. Xnornet:
Imagenet classification using binary convolutional neural networks. In ECCV, 2016.