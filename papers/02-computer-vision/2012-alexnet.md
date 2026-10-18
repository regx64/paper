# ImageNet Classification with Deep Convolutional Neural Networks (AlexNet, 2012)

| 항목 | 내용 |
|---|---|
| 저자 | Alex Krizhevsky, Ilya Sutskever, Geoffrey Hinton |
| 학회/저널 | NeurIPS 2012 |
| 링크 | [NeurIPS](https://proceedings.neurips.cc/paper/2012/hash/c399862d3b9d6b76c8436e924a68c45b-Abstract.html) |
| 난이도 | 🟢 |
| 사전 지식 | [Deep Learning (2015)](../01-foundations/2015-deep-learning.md)의 CNN 부분, [Dropout (2014)](../01-foundations/2014-dropout.md) |

## 한 줄 요약

크고 깊은 CNN을 **GPU로** 대규모 데이터셋(ImageNet)에서 학습해, 이미지 분류 대회에서 2등과 압도적인 차이로 우승하며 딥러닝 붐을 일으켰다.

## 왜 중요한가?

2012년 ImageNet 대회(ILSVRC-2012)에서 AlexNet의 top-5 오류율은 **15.3%**, 2등은 **26.2%** 였다. 2등을 비롯한 기존 방법은 사람이 설계한 특징에 기반했기 때문에, 이 결과는 "특징을 데이터에서 배우는 신경망이 사람이 만든 특징보다 낫다"는 것을 보여 준 결정적 사건이었다.
이후 컴퓨터 비전 연구는 빠르게 딥러닝 중심으로 바뀌었고, 다른 분야도 뒤따랐다.

> ImageNet 분류 과제: 약 120만 장의 학습 이미지를 1,000개 클래스로 분류. top-5 오류율은 모델이 고른 상위 5개 답 안에 정답이 없는 비율이다.

## 핵심 아이디어

AlexNet의 구조 자체는 LeNet(1998)과 크게 다르지 않다. 합성곱층 5개 + 완전연결층 3개, 파라미터 약 6,000만 개다. 성공의 비결은 **규모를 키우면서 학습이 되게 만든 여러 실용적 기법**에 있다.

| 기법 | 내용 | 지금도 쓰이나? |
|---|---|---|
| **ReLU 활성화 함수** | tanh 대신 max(0, x)를 사용. 기울기가 잘 사라지지 않아 학습이 몇 배 빠름 | ✅ 표준 |
| **GPU 2장으로 학습** | 당시 GPU(GTX 580) 메모리가 3GB뿐이라 신경망을 반으로 나눠 두 GPU에 올림. 학습에 5~6일 | GPU 학습은 표준, 이런 분할 방식은 X |
| **데이터 증강** | 이미지를 무작위로 잘라내고 좌우 반전, 색상 변형 | ✅ 표준 |
| **드롭아웃** | 완전연결층에 적용해 과적합 감소 | ✅ 널리 사용 |
| 국소 응답 정규화(LRN) | 인접 채널끼리 출력을 정규화 | ❌ 이후 배치 정규화로 대체 |
| 겹치는 풀링 | 풀링 창을 겹치게 배치 | ❌ 거의 안 씀 |

## 읽는 팁

- 아홉 쪽 정도로 짧고 문장이 쉬워서 **첫 "진짜 실험 논문"으로 좋다**.
- 먼저 읽기: 1장(서론), 3.1절(ReLU)과 해당 그래프, 3.5절(전체 구조)과 구조 그림, 4장(과적합 줄이기), 6장(결과)
- 건너뛰어도 됨: 3.2절(GPU 분할)과 3.3절(LRN)은 당시 하드웨어 사정에 맞춘 부분이라 가볍게 읽어도 된다
- 결과 절의 그림 중 **비슷한 이미지 검색 결과**(마지막 은닉층 벡터가 가까운 이미지끼리 묶은 그림)를 꼭 보자. 신경망이 픽셀이 아니라 "의미"로 이미지를 표현한다는 것을 보여 준다

## 함께 보면 좋은 자료

- [Dive into Deep Learning — AlexNet](https://d2l.ai/chapter_convolutional-modern/alexnet.html): LeNet과의 비교, 구현 코드
- [CS231n — Convolutional Networks](https://cs231n.github.io/convolutional-networks/): 합성곱, 풀링, 대표 CNN 구조 설명

## 이어서 읽을 논문

- [VGG (2014)](README.md): 3×3 필터만으로 더 깊게 쌓은 단순한 구조
- [ResNet (2015)](2015-resnet.md): 100층이 넘는 신경망을 학습 가능하게 만든 논문
