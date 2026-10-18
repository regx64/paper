# Deep Residual Learning for Image Recognition (ResNet, 2015)

| 항목 | 내용 |
|---|---|
| 저자 | Kaiming He, Xiangyu Zhang, Shaoqing Ren, Jian Sun |
| 학회/저널 | CVPR 2016 (최우수 논문상) |
| 링크 | [arXiv](https://arxiv.org/abs/1512.03385) |
| 난이도 | 🟡 |
| 사전 지식 | [AlexNet (2012)](2012-alexnet.md), VGG, 배치 정규화 |

## 한 줄 요약

층의 입력을 출력에 그대로 더해 주는 **지름길 연결(shortcut connection)** 을 추가해, 100층이 넘는 매우 깊은 신경망도 학습할 수 있게 만들었다.

## 왜 중요한가?

AlexNet(8층) → VGG(19층)로 이어지며 "깊을수록 좋다"는 것이 알려졌지만, 층을 더 쌓으면 오히려 성능이 떨어지는 문제가 있었다.
ResNet은 이 문제를 단순한 아이디어로 해결해 **152층** 신경망으로 ILSVRC-2015에서 우승했다(top-5 오류율 3.57%, 앙상블 기준).
더 중요한 것은 이 **잔차 연결(residual connection)** 이 이후 거의 모든 딥러닝 모델의 기본 부품이 되었다는 점이다. [트랜스포머](../03-sequence-and-nlp/2017-attention-is-all-you-need.md)의 모든 층에도 잔차 연결이 들어 있다.

## 핵심 아이디어

### 문제: 성능 저하(degradation)

논문의 첫 그림이 문제를 정확히 보여 준다. CIFAR-10에서 56층 신경망이 20층 신경망보다 **학습 오류도, 테스트 오류도** 높았다.
학습 오류까지 높다는 것은 과적합 때문이 아니라 **최적화 자체가 어렵다**는 뜻이다.

생각해 보면 이상한 일이다. 20층 신경망 위에 "입력을 그대로 내보내는 층(항등 함수)" 36개를 쌓으면, 적어도 20층과 같은 성능은 나와야 한다. 그런데 여러 비선형 층으로 항등 함수를 정확히 배우는 것조차 쉽지 않았던 것이다.

### 해결: 차이(잔차)만 배우게 하자

원하는 함수를 *H(x)* 라고 할 때, 층이 *H(x)* 를 직접 배우는 대신 **차이 *F(x) = H(x) − x*** 만 배우게 한다. 출력은 *F(x) + x* 가 된다.

```
 x ─────────────────┐ (지름길: 그대로 전달)
 │                  │
 └→ [층] → [층] → F(x) ─(+)→ F(x) + x
```

- 항등 함수가 최적이라면, 층은 *F(x)* = 0만 배우면 된다. 가중치를 0 쪽으로 보내는 것은 쉽다.
- 역전파 때 기울기가 지름길을 통해 **곧바로 앞쪽 층까지 전달**되므로, 깊어도 기울기가 잘 사라지지 않는다.
- 지름길은 단순한 덧셈이라 파라미터와 연산량이 거의 늘지 않는다.

### 병목 블록(bottleneck block)

50층 이상 모델에서는 1×1 → 3×3 → 1×1 합성곱으로 이루어진 블록을 쓴다. 1×1 합성곱으로 채널 수를 줄였다가 다시 늘려서 연산량을 아낀다.

## 읽는 팁

- 먼저 읽기: 첫 번째 그림(20층 vs 56층), 3.1~3.2절(잔차 학습과 지름길), 잔차 블록 그림, 4.1절의 일반 신경망 vs ResNet 학습 곡선 비교 그림
- 그다음: 네트워크 구조 표(ResNet-18/34/50/101/152의 층 구성)와 병목 블록 그림
- 건너뛰어도 됨: 지름길의 차원을 맞추는 세 가지 방법(A/B/C) 비교, 객체 탐지 결과(부록)
- CIFAR-10에서 1,202층까지 실험한 부분도 재미있다. 학습은 되지만 과적합 때문에 110층보다 성능이 나빴다

## 함께 보면 좋은 자료

- [Dive into Deep Learning — ResNet](https://d2l.ai/chapter_convolutional-modern/resnet.html): 잔차 블록 구현 코드
- [torchvision ResNet](https://pytorch.org/vision/stable/models/resnet.html): PyTorch에서 바로 쓸 수 있는 공식 구현과 사전학습 가중치

## 이어서 읽을 논문

- [Identity Mappings in Deep Residual Networks (2016)](https://arxiv.org/abs/1603.05027): 같은 저자들이 잔차 블록 안의 순서를 바꿔 더 잘 학습되게 개선
- [Densely Connected Convolutional Networks (DenseNet, 2016)](https://arxiv.org/abs/1608.06993): 지름길 연결을 극단적으로 확장
- [U-Net (2015)](2015-u-net.md): 디퓨전 모델에서 다시 등장하는 구조
- [Attention Is All You Need (2017)](../03-sequence-and-nlp/2017-attention-is-all-you-need.md): 잔차 연결이 트랜스포머에서 어떻게 쓰이는지 확인해 보자
