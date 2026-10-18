# Neural Machine Translation by Jointly Learning to Align and Translate (2014)

| 항목 | 내용 |
|---|---|
| 저자 | Dzmitry Bahdanau, Kyunghyun Cho, Yoshua Bengio |
| 학회/저널 | ICLR 2015 |
| 링크 | [arXiv](https://arxiv.org/abs/1409.0473) |
| 난이도 | 🟡 |
| 사전 지식 | [Sequence to Sequence Learning (2014)](2014-seq2seq.md), [LSTM (1997)](1997-lstm.md) |

## 한 줄 요약

번역할 단어를 하나 만들 때마다 입력 문장의 **어느 부분을 집중해서 볼지** 신경망이 스스로 정하게 하는 **어텐션(attention)** 을 도입해, 긴 문장 번역 성능을 크게 높였다.

## 왜 중요한가?

[Seq2Seq](2014-seq2seq.md)는 입력 문장 전체를 **고정 길이 벡터 하나**에 담아야 해서, 문장이 길어질수록 번역 품질이 급격히 떨어졌다.
이 논문은 디코더가 매 단계 입력 문장 전체를 다시 훑어보며 **필요한 부분을 골라 쓰게** 해서 이 병목을 없앴다.
여기서 처음 제안된 어텐션 개념은 3년 뒤 "어텐션만 있으면 된다"는 [트랜스포머](2017-attention-is-all-you-need.md)로 발전해, 현대 AI의 핵심 메커니즘이 되었다. 공동 저자인 조경현 교수는 한국인 연구자로, GRU를 제안한 연구자이기도 하다.

## 핵심 아이디어

### 1. 사람이 번역하는 방식

사람은 긴 문장을 번역할 때 전체를 한 번 읽고 외운 다음 번역하지 않는다. 번역할 단어마다 원문의 **해당 부분을 다시 보면서** 번역한다. 어텐션은 이 과정을 흉내 낸다.

### 2. 인코더: 단어마다 벡터 하나씩

인코더로 **양방향 RNN**을 쓴다. 앞→뒤, 뒤→앞으로 각각 읽은 결과를 합쳐서, 입력의 각 단어마다 "그 단어와 주변 문맥"을 담은 벡터 *h*_j를 만든다. 이제 문장 전체를 벡터 하나로 압축하지 않고, **단어 수만큼의 벡터**를 남겨 둔다.

### 3. 디코더: 매 단계 어텐션으로 문맥 벡터 만들기

출력의 *i*번째 단어를 만들 때:

1. **점수 계산**: 디코더의 직전 상태 *s*_{i−1}과 입력의 각 단어 벡터 *h*_j가 얼마나 관련 있는지 작은 신경망으로 점수를 매긴다
   > *e*_ij = *v*ᵀ tanh(*W* *s*_{i−1} + *U* *h*_j)  (이 형태를 **덧셈 어텐션**, additive attention이라고 부른다)
2. **가중치로 변환**: softmax로 점수를 합이 1인 가중치 α_ij로 바꾼다
3. **문맥 벡터**: 입력 단어 벡터들의 가중합 *c*_i = Σ α_ij *h*_j 를 만든다
4. 이 문맥 벡터로 다음 단어를 생성한다

문맥 벡터가 **출력 단어마다 달라지는 것**이 핵심이다.

### 4. 정렬(alignment)이 저절로 학습된다

α_ij를 그림으로 그리면, "출력 단어 *i*를 만들 때 입력 단어 *j*를 얼마나 봤는지"가 보인다. 영어 "European Economic Area"를 프랑스어 "zone économique européenne"로 번역할 때 **단어 순서가 뒤바뀐 것까지** 올바르게 대응시켰다. 아무도 단어 대응 관계를 알려 주지 않았는데 번역을 배우면서 함께 학습한 것이다.

## 읽는 팁

- 먼저 읽기: 1장(서론), 3장(정렬과 번역을 함께 학습)과 어텐션 구조 그림, 결과 절의 **문장 길이별 BLEU 그래프**(어텐션 모델은 긴 문장에서도 성능이 유지됨)와 **어텐션 가중치 시각화 그림**
- 건너뛰어도 됨: 2장의 기존 RNN 인코더-디코더 배경 설명(Seq2Seq를 읽었다면), 부록의 모델 구조·학습 세부 사항
- 트랜스포머의 Query·Key·Value 어텐션과 비교해 보자. 디코더 상태가 Query, 인코더 단어 벡터가 Key와 Value 역할을 한다

## 함께 보면 좋은 자료

- [Jay Alammar — Visualizing A Neural Machine Translation Model](https://jalammar.github.io/visualizing-neural-machine-translation-mechanics-of-seq2seq-models-with-attention/): 어텐션이 동작하는 과정을 애니메이션으로 설명
- [Lilian Weng — Attention? Attention!](https://lilianweng.github.io/posts/2018-06-24-attention/): 여러 종류의 어텐션을 한 번에 정리
- [Dive into Deep Learning — The Bahdanau Attention Mechanism](https://d2l.ai/chapter_attention-mechanisms-and-transformers/bahdanau-attention.html)

## 이어서 읽을 논문

- [Effective Approaches to Attention-based Neural Machine Translation (2015)](https://arxiv.org/abs/1508.04025): 더 단순한 **곱셈(내적) 어텐션** 제안
- [Attention Is All You Need (2017)](2017-attention-is-all-you-need.md): RNN을 없애고 어텐션만으로
