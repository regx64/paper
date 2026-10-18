# 6단계. 대규모 언어 모델(LLM)

> ChatGPT는 어떻게 만들어졌나?

## 이 단계의 목표

- 모델 크기, 데이터, 연산량과 성능의 관계(스케일링 법칙)를 이해한다.
- 사전학습된 언어 모델을 **사람의 지시를 따르는 모델**로 만드는 방법(RLHF)을 안다.
- LLM을 실제로 활용하는 기법(LoRA 파인튜닝, RAG, 프롬프팅)을 안다.

## 사전 지식

- [3단계 시퀀스와 NLP](../03-sequence-and-nlp/) (특히 Transformer, GPT-3)
- [5단계 강화학습](../05-reinforcement-learning/)의 PPO (InstructGPT를 읽을 때)

## 읽는 순서

| # | 논문 | 연도 | 난이도 | 링크 | 노트 |
|---|---|---|---|---|---|
| 1 | Scaling Laws for Neural Language Models | 2020 | 🟡 | [arXiv](https://arxiv.org/abs/2001.08361) | — |
| 2 | Training Compute-Optimal Large Language Models (Chinchilla) | 2022 | 🟡 | [arXiv](https://arxiv.org/abs/2203.15556) | — |
| 3 | ⭐ Training Language Models to Follow Instructions with Human Feedback (InstructGPT) | 2022 | 🟡 | [arXiv](https://arxiv.org/abs/2203.02155) | — |
| 4 | Chain-of-Thought Prompting Elicits Reasoning in Large Language Models | 2022 | 🟢 | [arXiv](https://arxiv.org/abs/2201.11903) | — |
| 5 | ⭐ LoRA: Low-Rank Adaptation of Large Language Models | 2021 | 🟡 | [arXiv](https://arxiv.org/abs/2106.09685) | — |
| 6 | Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks (RAG) | 2020 | 🟡 | [arXiv](https://arxiv.org/abs/2005.11401) | — |
| 7 | LLaMA: Open and Efficient Foundation Language Models | 2023 | 🟢 | [arXiv](https://arxiv.org/abs/2302.13971) | — |

- 1~2번은 "어떻게 크게 만들까", 3~4번은 "어떻게 말을 잘 듣게 할까", 5~7번은 "어떻게 활용할까"에 대한 논문입니다.
- 3번 InstructGPT는 ChatGPT의 직계 조상으로, 이 단계의 핵심입니다.

## 이 단계를 마치면

- 사전학습 → 지시 학습 → RLHF로 이어지는 ChatGPT류 모델의 학습 과정을 설명할 수 있습니다.
- 더 나아가기: 최신 논문은 추후 `recent/` 폴더에서 다룰 예정입니다.
