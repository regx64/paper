# LLaMA: Open and Efficient Foundation Language Models (2023)

| 항목 | 내용 |
|---|---|
| 저자 | Hugo Touvron, Thibaut Lavril, Gautier Izacard 외 (Meta AI) |
| 학회/저널 | arXiv (2023) |
| 링크 | [arXiv](https://arxiv.org/abs/2302.13971) |
| 난이도 | 🟢 |
| 사전 지식 | [GPT-3 (2020)](../03-sequence-and-nlp/2020-gpt-3.md), [Chinchilla (2022)](2022-chinchilla.md) |

## 한 줄 요약

**공개된 데이터만으로** 70억~650억 파라미터 모델을 Chinchilla 비율보다 훨씬 많은 데이터로 오래 학습시켰더니, 130억 모델이 1,750억 GPT-3보다 대부분의 벤치마크에서 좋았다. 그리고 연구자들에게 가중치를 공개했다.

## 왜 중요한가?

2023년 초까지 최고 수준의 LLM은 GPT-3, PaLM처럼 대부분 **비공개**였다. 연구자들이 모델 내부를 들여다보거나, 직접 파인튜닝하거나, 개선 연구를 하기 어려웠다.
LLaMA는 성능 좋은 모델의 **가중치를 연구자들에게 공개**하면서 상황을 바꿨다. 공개 직후 이를 바탕으로 한 Alpaca, Vicuna 같은 파인튜닝 모델, 노트북에서 LLM을 돌리는 llama.cpp 같은 도구가 쏟아져 나왔다. [LoRA](2021-lora.md) 같은 효율적 파인튜닝 기법도 LLaMA와 함께 널리 퍼졌다.
이후 Llama 2(상업적 사용 허용), Llama 3로 이어지며 **오픈 웨이트 LLM 생태계**의 출발점이 되었다.

## 핵심 아이디어

### 1. 사용(추론) 비용까지 고려한 학습

[Chinchilla](2022-chinchilla.md)는 "**학습** 예산이 정해졌을 때 최적인 크기"를 알려 준다. 하지만 모델은 학습 후 수없이 **사용**된다. 사용 비용은 모델 크기에 비례하므로, 같은 성능이라면 **작은 모델이 훨씬 경제적**이다.

LLaMA는 이 관점에서, 작은 모델을 Chinchilla 비율보다 **훨씬 오래** 학습시켰다.

| 모델 | 파라미터 | 학습 토큰 | 파라미터당 토큰 |
|---|---|---|---|
| LLaMA-7B | 70억 | 1.0조 | 약 140 |
| LLaMA-13B | 130억 | 1.0조 | 약 77 |
| LLaMA-33B | 330억 | 1.4조 | 약 42 |
| LLaMA-65B | 650억 | 1.4조 | 약 22 |

(Chinchilla 비율은 파라미터당 약 20토큰)
70억 모델은 1조 토큰을 학습한 뒤에도 성능이 계속 좋아지고 있었다. 작은 모델도 오래 학습하면 계속 좋아진다는 뜻이다.

### 2. 공개 데이터만 사용

| 데이터 | 비율 |
|---|---|
| CommonCrawl (웹 문서, 필터링) | 67% |
| C4 (정제된 웹 문서) | 15% |
| GitHub (코드) | 4.5% |
| 위키백과 (20개 언어) | 4.5% |
| 책 (Gutenberg, Books3) | 4.5% |
| arXiv (논문) | 2.5% |
| StackExchange (질의응답) | 2% |

누구나 구할 수 있는 데이터만으로 최고 수준에 도달할 수 있음을 보였다는 점이 중요하다.

### 3. 구조: 검증된 개선 사항의 조합

기본은 GPT 계열의 트랜스포머 디코더이고, 이전 연구들에서 효과가 확인된 개선을 모아 적용했다. 이 조합은 이후 공개 LLM 대부분의 **표준 구조**가 되었다.

| 변경 | 내용 | 출처 |
|---|---|---|
| 사전 정규화 + **RMSNorm** | 각 하위 층의 입력을 정규화. 층 정규화를 단순화한 RMSNorm 사용 | GPT-3, [RMSNorm](https://arxiv.org/abs/1910.07467) |
| **SwiGLU** 활성화 함수 | ReLU 대신 사용. 성능 향상 | PaLM, [GLU Variants](https://arxiv.org/abs/2002.05202) |
| **회전 위치 임베딩 (RoPE)** | 절대 위치 임베딩 대신, 벡터를 위치에 따라 회전시켜 상대 위치 정보를 넣음 | [RoFormer](https://arxiv.org/abs/2104.09864) |

### 4. 결과

- **LLaMA-13B**가 10배 이상 큰 GPT-3(1,750억)보다 대부분의 벤치마크에서 좋음 → GPU 한 장에서 돌릴 수 있는 크기로 GPT-3 수준
- **LLaMA-65B**는 Chinchilla-70B, PaLM-540B와 경쟁할 만한 수준
- 학습에는 A100 GPU 2,048장으로 65B 모델 기준 약 21일이 걸렸다

## 읽는 팁

- 짧고 읽기 쉬운 논문이다
- 먼저 읽기: 1장(서론: 추론 비용 관점의 학습 철학), 2.1절(데이터 구성 표), 2.2절(구조 변경 사항), 학습 손실 그래프(학습 토큰이 늘어도 계속 내려가는 곡선)
- 그다음: 3장 결과 표 중 상식 추론·질의응답 비교, 5장(편향·유해성 평가)
- 건너뛰어도 됨: 2.4절 효율적 구현(메모리 최적화) 세부 사항, 개별 벤치마크 세부 설정
- 4장의 간단한 지시 학습(instruction finetuning) 실험은 [InstructGPT](2022-instructgpt.md)와 연결해 보면 좋다

## 함께 보면 좋은 자료

- [facebookresearch/llama](https://github.com/facebookresearch/llama): 공식 코드
- [Stanford Alpaca](https://crfm.stanford.edu/2023/03/13/alpaca.html): LLaMA-7B를 지시 데이터로 파인튜닝한 초기 사례. 공개 모델 생태계가 어떻게 시작되었는지 보여 줌
- [Andrej Karpathy — Let's build GPT](https://www.youtube.com/watch?v=kCc8FmEb1nY): 디코더 트랜스포머를 직접 구현하며 LLaMA의 기본 구조 이해하기

## 이어서 읽을 논문

- [Llama 2 (2023)](https://arxiv.org/abs/2307.09288): 상업적 사용 허용, RLHF로 학습한 대화 모델 포함, 학습 과정 상세 공개
- [The Llama 3 Herd of Models (2024)](https://arxiv.org/abs/2407.21783): 15조 토큰 이상 학습, 최대 4,050억 파라미터
- [QLoRA (2023)](https://arxiv.org/abs/2305.14314): LLaMA를 GPU 한 장으로 파인튜닝
