# Gradient-Based Learning Applied to Document Recognition (LeNet, 1998)

| 항목 | 내용 |
|---|---|
| 저자 | Yann LeCun, Léon Bottou, Yoshua Bengio, Patrick Haffner |
| 학회/저널 | *Proceedings of the IEEE* 86(11), 1998 |
| 링크 | [DOI](https://doi.org/10.1109/5.726791) |
| 난이도 | 🟡 |
| 사전 지식 | [역전파 (1986)](1986-backpropagation.md), [Deep Learning (2015)](2015-deep-learning.md)의 CNN 부분 |

## 한 줄 요약

손글씨 숫자 인식에 **합성곱 신경망(CNN) LeNet-5**를 역전파로 학습시켜, 사람이 설계한 특징을 쓰는 기존 방법보다 좋은 성능을 냈고, 실제 은행 수표 인식 시스템에 쓰였다.

## 왜 중요한가?

오늘날 CNN의 기본 구성 요소(합성곱층, 풀링층, 마지막의 완전연결층)를 정립한 논문이다. [AlexNet (2012)](../02-computer-vision/2012-alexnet.md)은 사실상 LeNet을 크게 키우고 GPU로 학습한 것이라고 볼 수 있다.
또 이 논문에서 소개한 **MNIST** 데이터셋(손글씨 숫자 학습용 6만 장, 테스트용 1만 장)은 지금까지도 머신러닝 입문 예제의 표준으로 쓰인다.

## 핵심 아이디어

### 왜 완전연결 신경망으로는 부족한가?

이미지를 픽셀 벡터로 펴서 완전연결 신경망에 넣으면

1. 파라미터가 너무 많아지고,
2. 숫자가 몇 픽셀만 옆으로 움직여도 완전히 다른 입력이 되며,
3. 이웃 픽셀끼리 관련이 깊다는 이미지의 구조를 활용하지 못한다.

### CNN의 세 가지 아이디어

| 아이디어 | 내용 | 효과 |
|---|---|---|
| **국소 수용 영역** (local receptive field) | 각 뉴런은 이미지의 작은 영역(예: 5×5)만 본다 | 모서리, 끝점 같은 지역적 특징 검출 |
| **가중치 공유** (weight sharing) | 같은 필터를 이미지 전체에 걸쳐 사용한다 | 파라미터 수가 크게 줄고, 특징이 어디에 있든 검출 |
| **서브샘플링** (subsampling, 지금의 풀링) | 특징 맵의 해상도를 줄인다 | 작은 위치 변화와 왜곡에 강해짐 |

### LeNet-5 구조

```
입력 32×32 → C1 합성곱 (6개 특징 맵) → S2 서브샘플링
           → C3 합성곱 (16개) → S4 서브샘플링
           → C5 (120) → F6 완전연결 (84) → 출력 (10개 숫자)
```

학습 가능한 층이 7개다. 층을 지날수록 특징 맵의 크기는 작아지고 개수는 많아진다. 이 패턴은 현대 CNN에도 그대로 남아 있다.

## 읽는 팁

- **46쪽에 달하는 긴 논문이지만, 앞부분만 읽으면 충분하다.**
- 먼저 읽기: 1장(서론: 특징을 직접 설계하는 대신 학습하자는 주장), 2장(CNN과 LeNet-5)과 LeNet-5 구조 그림
- 그다음: 3장의 MNIST 결과 비교 그래프. 선형 분류기, k-NN, SVM 등 여러 방법과 오류율을 비교한다
- 건너뛰어도 됨: 4장 이후(그래프 변환 네트워크, 문자열 분할, 수표 인식 시스템). 당시의 문서 인식 시스템 전체를 다루는 부분이라 입문 단계에서는 필요 없다

## 함께 보면 좋은 자료

- [Dive into Deep Learning — LeNet](https://d2l.ai/chapter_convolutional-neural-networks/lenet.html): LeNet 구현과 학습 코드
- [CS231n — Convolutional Networks](https://cs231n.github.io/convolutional-networks/): 합성곱과 풀링의 계산 방식

## 이어서 읽을 논문

- [AlexNet (2012)](../02-computer-vision/2012-alexnet.md): LeNet을 크게 키워 ImageNet에 적용
- [Dropout (2014)](2014-dropout.md): 큰 신경망의 과적합 방지
