# Efficient Estimation of Word Representations in Vector Space (word2vec, 2013)

| 항목 | 내용 |
|---|---|
| 저자 | Tomas Mikolov, Kai Chen, Greg Corrado, Jeffrey Dean |
| 학회/저널 | ICLR 2013 Workshop |
| 링크 | [arXiv](https://arxiv.org/abs/1301.3781) |
| 난이도 | 🟢 |
| 사전 지식 | [Deep Learning (2015)](../01-foundations/2015-deep-learning.md)의 분산 표현 부분, 소프트맥스 |

## 한 줄 요약

"주변 단어로 가운데 단어를 맞히기" 같은 아주 단순한 과제로 대량의 텍스트를 학습하면, 단어의 **의미를 담은 벡터(임베딩)** 를 빠르게 얻을 수 있다.

## 왜 중요한가?

컴퓨터는 단어를 숫자로 바꿔야 다룰 수 있다. 가장 단순한 방법은 원-핫 벡터(단어마다 번호를 하나씩 주는 방식)지만, 이 방식에서는 "고양이"와 "강아지"가 "고양이"와 "자동차"만큼 서로 다르다.
word2vec은 **비슷한 의미의 단어가 가까운 벡터**를 갖도록 학습하는 방법을, 이전 신경망 언어 모델보다 훨씬 **빠르고 단순하게** 만들었다. 덕분에 수십억 단어 규모의 데이터로 학습할 수 있었다.
"단어를 벡터로 바꾼 뒤 신경망에 넣는다"는 방식은 이후 모든 NLP 모델의 출발점이 되었고, 오늘날 LLM의 입력층(토큰 임베딩)도 같은 아이디어다.

## 핵심 아이디어

### 분포 가설: 단어의 의미는 주변 단어가 결정한다

"나는 아침에 ___를 마셨다"의 빈칸에는 "커피", "우유", "주스"처럼 비슷한 단어가 들어간다. 그렇다면 **비슷한 문맥에 나오는 단어끼리 비슷한 벡터**를 갖게 학습하면 된다.

### 두 가지 모델

| 모델 | 과제 | 예시 (`the cat sat on the mat`, 가운데 단어 `sat`) |
|---|---|---|
| **CBOW** (Continuous Bag-of-Words) | 주변 단어들로 가운데 단어 맞히기 | `the, cat, on, the` → `sat` |
| **Skip-gram** | 가운데 단어로 주변 단어 맞히기 | `sat` → `the, cat, on, the` |

두 모델 모두 은닉층이 사실상 하나뿐인 아주 얕은 구조다. 논문의 핵심 주장은 "복잡한 신경망보다 **단순한 모델을 더 많은 데이터로** 학습하는 것이 낫다"는 것이다.

### 벡터 산술: 단어로 계산하기

학습된 벡터는 놀라운 성질을 보인다.

> vector("King") − vector("Man") + vector("Woman") ≈ vector("Queen")
> vector("Paris") − vector("France") + vector("Italy") ≈ vector("Rome")

"남성 → 여성", "나라 → 수도" 같은 관계가 벡터 공간에서 **일정한 방향**으로 표현된다는 뜻이다. 논문은 이런 유추 문제를 모은 테스트셋을 만들어 임베딩의 품질을 평가했다.

## 읽는 팁

- 먼저 읽기: 1장(서론), 3장(CBOW와 Skip-gram)과 두 모델의 구조 그림, 결과 절의 단어 관계 예시 표
- 건너뛰어도 됨: 2장의 기존 모델(NNLM, RNNLM) 계산 복잡도 분석
- **같은 해에 나온 후속 논문을 꼭 함께 보자.** 이 논문에는 지금 word2vec이라고 하면 떠올리는 핵심 기법(네거티브 샘플링)이 아직 없다. 실제로 널리 쓰인 버전은 아래 "이어서 읽을 논문"의 첫 번째 논문이다

## 함께 보면 좋은 자료

- [Jay Alammar — The Illustrated Word2vec](https://jalammar.github.io/illustrated-word2vec/): 그림으로 설명하는 word2vec. 입문자에게 가장 추천
- [TensorFlow — word2vec 튜토리얼](https://www.tensorflow.org/text/tutorials/word2vec): Skip-gram과 네거티브 샘플링 구현
- [딥 러닝을 이용한 자연어 처리 입문 (WikiDocs)](https://wikidocs.net/book/2155): 한국어 NLP 입문서. 워드 임베딩 장 참고

## 이어서 읽을 논문

- [Distributed Representations of Words and Phrases and their Compositionality (2013)](https://arxiv.org/abs/1310.4546): 네거티브 샘플링, 빈도 높은 단어 서브샘플링, 구(phrase) 임베딩을 추가한 word2vec의 완성판
- [GloVe (2014)](https://nlp.stanford.edu/projects/glove/): 단어 동시 등장 통계를 직접 이용하는 또 다른 임베딩 방법
- [Sequence to Sequence Learning (2014)](2014-seq2seq.md): 단어 벡터를 이어 붙여 문장을 다루는 모델
