# 1단계. 딥러닝 기초

> 신경망은 어떻게 학습하나?

## 이 단계의 목표

- 신경망이 데이터로부터 **어떻게 학습하는지**(역전파, 경사 하강법) 이해한다.
- 학습을 **잘 되게 만드는 기법**(드롭아웃, Adam, 배치 정규화)이 왜 필요한지 안다.

## 사전 지식

- 미분과 연쇄 법칙, 행렬 곱셈
- 손실 함수, 경사 하강법의 기본 개념

## 읽는 순서

| # | 논문 | 연도 | 난이도 | 링크 | 노트 |
|---|---|---|---|---|---|
| 1 | ⭐ Deep Learning (LeCun, Bengio, Hinton) | 2015 | 🟢 | [Nature](https://www.nature.com/articles/nature14539) | [노트](2015-deep-learning.md) |
| 2 | Learning Representations by Back-propagating Errors | 1986 | 🟡 | [Nature](https://www.nature.com/articles/323533a0) | — |
| 3 | Gradient-Based Learning Applied to Document Recognition (LeNet) | 1998 | 🟡 | [DOI](https://doi.org/10.1109/5.726791) | — |
| 4 | ⭐ Dropout: A Simple Way to Prevent Neural Networks from Overfitting | 2014 | 🟢 | [JMLR](https://jmlr.org/papers/v15/srivastava14a.html) | [노트](2014-dropout.md) |
| 5 | ⭐ Adam: A Method for Stochastic Optimization | 2014 | 🟡 | [arXiv](https://arxiv.org/abs/1412.6980) | [노트](2014-adam.md) |
| 6 | Batch Normalization | 2015 | 🟡 | [arXiv](https://arxiv.org/abs/1502.03167) | — |

**1번(Deep Learning 리뷰 논문)을 첫 논문으로 추천합니다.** 분야 전체를 짧게 훑어 주기 때문에, 이후 논문을 읽을 때 지도 역할을 합니다.

## 이 단계를 마치면

- "신경망을 학습시킨다"는 말이 구체적으로 무엇을 뜻하는지 설명할 수 있습니다.
- 다음 단계: [2단계 컴퓨터 비전](../02-computer-vision/) 또는 [3단계 시퀀스와 NLP](../03-sequence-and-nlp/)
