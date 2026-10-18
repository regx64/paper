# 2단계. 컴퓨터 비전

> 모델은 이미지를 어떻게 이해하나?

## 이 단계의 목표

- 합성곱 신경망(CNN)이 이미지에서 특징을 뽑아내는 방식을 이해한다.
- 신경망을 **깊게** 쌓을 때 생기는 문제와 해결책(잔차 연결)을 안다.
- 분류 외에 분할(segmentation), 객체 탐지(detection) 같은 과제가 있음을 안다.

## 사전 지식

- [1단계 딥러닝 기초](../01-foundations/), 특히 LeNet

## 읽는 순서

| # | 논문 | 연도 | 난이도 | 링크 | 노트 |
|---|---|---|---|---|---|
| 1 | ⭐ ImageNet Classification with Deep Convolutional Neural Networks (AlexNet) | 2012 | 🟢 | [NeurIPS](https://proceedings.neurips.cc/paper/2012/hash/c399862d3b9d6b76c8436e924a68c45b-Abstract.html) | [노트](2012-alexnet.md) |
| 2 | Very Deep Convolutional Networks for Large-Scale Image Recognition (VGG) | 2014 | 🟢 | [arXiv](https://arxiv.org/abs/1409.1556) | — |
| 3 | ⭐ Deep Residual Learning for Image Recognition (ResNet) | 2015 | 🟡 | [arXiv](https://arxiv.org/abs/1512.03385) | [노트](2015-resnet.md) |
| 4 | U-Net: Convolutional Networks for Biomedical Image Segmentation | 2015 | 🟡 | [arXiv](https://arxiv.org/abs/1505.04597) | — |
| 5 | You Only Look Once: Unified, Real-Time Object Detection (YOLO) | 2015 | 🟡 | [arXiv](https://arxiv.org/abs/1506.02640) | — |
| 6 | An Image is Worth 16x16 Words (ViT) | 2020 | 🟡 | [arXiv](https://arxiv.org/abs/2010.11929) | — |

6번 ViT는 트랜스포머를 이미지에 적용한 논문이므로, [3단계](../03-sequence-and-nlp/)의 Transformer를 읽은 뒤에 보는 것을 추천합니다.

## 이 단계를 마치면

- ResNet의 잔차 연결이 왜 이후 거의 모든 모델(트랜스포머 포함)에 쓰이는지 설명할 수 있습니다.
- 다음 단계: [4단계 생성 모델](../04-generative-models/)
