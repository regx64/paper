# 3단계. 시퀀스와 자연어 처리

> 모델은 언어를 어떻게 다루나?

## 이 단계의 목표

- 단어를 숫자 벡터로 바꾸는 **임베딩**의 개념을 이해한다.
- RNN → 어텐션 → 트랜스포머로 이어지는 흐름을 따라간다.
- **사전학습(pre-training)** 후 활용하는 방식(BERT, GPT)을 안다.

## 사전 지식

- [1단계 딥러닝 기초](../01-foundations/)

## 읽는 순서

| # | 논문 | 연도 | 난이도 | 링크 | 노트 |
|---|---|---|---|---|---|
| 1 | ⭐ Efficient Estimation of Word Representations in Vector Space (word2vec) | 2013 | 🟢 | [arXiv](https://arxiv.org/abs/1301.3781) | [노트](2013-word2vec.md) |
| 2 | Long Short-Term Memory (LSTM) | 1997 | 🔴 | [DOI](https://doi.org/10.1162/neco.1997.9.8.1735) | — |
| 3 | Sequence to Sequence Learning with Neural Networks | 2014 | 🟢 | [arXiv](https://arxiv.org/abs/1409.3215) | — |
| 4 | Neural Machine Translation by Jointly Learning to Align and Translate | 2014 | 🟡 | [arXiv](https://arxiv.org/abs/1409.0473) | — |
| 5 | ⭐ Attention Is All You Need (Transformer) | 2017 | 🟡 | [arXiv](https://arxiv.org/abs/1706.03762) | [노트](2017-attention-is-all-you-need.md) |
| 6 | ⭐ BERT: Pre-training of Deep Bidirectional Transformers | 2018 | 🟡 | [arXiv](https://arxiv.org/abs/1810.04805) | [노트](2018-bert.md) |
| 7 | Language Models are Unsupervised Multitask Learners (GPT-2) | 2019 | 🟢 | [OpenAI](https://cdn.openai.com/better-language-models/language_models_are_unsupervised_multitask_learners.pdf) | — |
| 8 | Language Models are Few-Shot Learners (GPT-3) | 2020 | 🟡 | [arXiv](https://arxiv.org/abs/2005.14165) | — |

- 2번 LSTM 원문은 입문자에게 어렵습니다. 원문 대신 해설 자료로 개념만 잡아도 충분합니다.
- 5번 Transformer는 이 저장소에서 **가장 중요한 논문 중 하나**입니다. 이후 거의 모든 단계에서 다시 등장합니다.
- 8번 GPT-3는 매우 긴 논문이므로 앞부분(1~3장) 위주로 읽어도 됩니다.

## 이 단계를 마치면

- "어텐션"이 무엇을 계산하는지, 트랜스포머가 왜 RNN을 대체했는지 설명할 수 있습니다.
- 다음 단계: [6단계 대규모 언어 모델](../06-large-language-models/) 또는 [4단계 생성 모델](../04-generative-models/)
