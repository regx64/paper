# Attention Is All You Need (Transformer, 2017)

| 항목 | 내용 |
|---|---|
| 저자 | Ashish Vaswani, Noam Shazeer, Niki Parmar, Jakob Uszkoreit, Llion Jones, Aidan N. Gomez, Łukasz Kaiser, Illia Polosukhin |
| 학회/저널 | NeurIPS 2017 |
| 링크 | [arXiv](https://arxiv.org/abs/1706.03762) |
| 난이도 | 🟡 |
| 사전 지식 | [word2vec (2013)](2013-word2vec.md), Seq2Seq와 어텐션(Bahdanau, 2014), [ResNet (2015)](../02-computer-vision/2015-resnet.md)의 잔차 연결 |

## 한 줄 요약

RNN 없이 **어텐션만으로** 문장을 처리하는 구조, 트랜스포머(Transformer)를 제안했다. 번역 성능이 더 좋으면서 병렬 처리가 가능해 학습이 훨씬 빨랐다.

## 왜 중요한가?

이 저장소에서 **가장 중요한 논문 중 하나**다. BERT, GPT, ChatGPT 같은 언어 모델은 물론이고 이미지(ViT), 이미지 생성(디퓨전 모델의 일부), 음성, 단백질 구조 예측까지 트랜스포머가 표준 구조가 되었다.

당시 번역 모델은 RNN 기반이었다. RNN은 단어를 **하나씩 순서대로** 처리하기 때문에

1. GPU로 병렬 처리하기 어려워 학습이 느렸고,
2. 문장이 길어지면 앞부분 정보가 희미해졌다.

트랜스포머는 모든 단어가 다른 모든 단어를 **한 번에** 바라보게 만들어 두 문제를 동시에 해결했다. WMT 2014 영어→독일어 번역에서 28.4 BLEU로 당시 최고 기록을 세웠고, 학습 비용은 기존 최고 모델들보다 훨씬 적었다.

## 핵심 아이디어

### 1. 셀프 어텐션(self-attention): 문장 안에서 서로를 참조하기

"The animal didn't cross the street because **it** was too tired"에서 `it`의 의미를 알려면 `animal`을 봐야 한다. 셀프 어텐션은 각 단어가 문장의 **모든 단어와의 관련도**를 계산해, 관련 높은 단어의 정보를 많이 가져오게 한다.

각 단어 벡터에서 세 가지 벡터를 만든다.

| 벡터 | 비유 (도서관 검색) |
|---|---|
| Query (Q) | 내가 찾고 싶은 것 (검색어) |
| Key (K) | 각 단어가 가진 "색인 카드" |
| Value (V) | 각 단어가 실제로 전달할 내용 |

> **Attention(Q, K, V) = softmax(QKᵀ / √dₖ) · V**

- QKᵀ: 검색어와 각 색인 카드의 유사도(내적)
- √dₖ로 나누기: 벡터 차원 dₖ가 크면 내적 값이 너무 커져 softmax가 한쪽으로 쏠리므로 크기를 줄여 줌
- softmax: 유사도를 합이 1인 가중치로 바꿈
- · V: 가중치만큼 각 단어의 내용을 섞어서 가져옴

### 2. 멀티 헤드 어텐션(multi-head attention)

어텐션을 한 번만 하지 않고 **8개의 "헤드"로 나눠 병렬로** 한다. 어떤 헤드는 문법 관계를, 어떤 헤드는 대명사가 가리키는 대상을 보는 식으로, 서로 다른 관계를 동시에 볼 수 있다.

### 3. 위치 인코딩(positional encoding)

어텐션은 단어 순서를 모른다("개가 사람을 물었다"와 "사람이 개를 물었다"를 구분 못 함). 그래서 각 위치마다 고유한 사인·코사인 패턴의 벡터를 단어 벡터에 **더해서** 순서 정보를 넣는다.

### 4. 전체 구조

```
[인코더 × 6층]                        [디코더 × 6층]
 셀프 어텐션                           마스크된 셀프 어텐션 (앞 단어만 보기)
 → 피드포워드 신경망                   → 인코더-디코더 어텐션 (원문 참조)
                                      → 피드포워드 신경망
 (모든 하위 층에 잔차 연결 + 층 정규화)
```

- **인코더**: 입력 문장(예: 영어)을 이해
- **디코더**: 출력 문장(예: 독일어)을 한 단어씩 생성. 아직 생성하지 않은 미래 단어는 못 보도록 가린다(마스킹)
- 이후 [BERT](2018-bert.md)는 인코더만, GPT 계열은 디코더만 가져다 쓴다

## 읽는 팁

- 먼저 읽기: 3장 전체(모델 구조)와 첫 두 그림(전체 구조도, scaled dot-product 어텐션과 멀티 헤드 어텐션). **이 논문은 3장이 전부**라고 해도 될 정도다
- 그다음: 4장(왜 셀프 어텐션인가: RNN, CNN과 계산량·경로 길이 비교 표)
- 건너뛰어도 됨: 5장 학습 세부 사항(학습률 스케줄 등), 6장 실험 결과의 세부 수치
- 원문만으로는 어려울 수 있다. **아래 "Illustrated Transformer"를 먼저 보고 논문을 읽는 것을 강력 추천**한다

## 함께 보면 좋은 자료

- [Jay Alammar — The Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/): 트랜스포머 해설의 고전. 가장 먼저 볼 자료
- [The Annotated Transformer (Harvard NLP)](https://nlp.seas.harvard.edu/annotated-transformer/): 논문 문장마다 PyTorch 코드를 붙여 한 줄씩 구현
- [Andrej Karpathy — Let's build GPT: from scratch, in code, spelled out](https://www.youtube.com/watch?v=kCc8FmEb1nY): 디코더 전용 트랜스포머를 직접 코딩하는 영상
- [Dive into Deep Learning — The Transformer Architecture](https://d2l.ai/chapter_attention-mechanisms-and-transformers/transformer.html)
- [딥 러닝을 이용한 자연어 처리 입문 (WikiDocs)](https://wikidocs.net/book/2155): 한국어 해설. 트랜스포머 장 참고

## 이어서 읽을 논문

- [BERT (2018)](2018-bert.md): 트랜스포머 인코더로 사전학습
- [GPT-2 (2019)](2019-gpt-2.md), [GPT-3 (2020)](2020-gpt-3.md): 트랜스포머 디코더로 사전학습
- [ViT (2020)](../02-computer-vision/2020-vit.md): 트랜스포머를 이미지에 적용
