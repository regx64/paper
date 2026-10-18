# Training Language Models to Follow Instructions with Human Feedback (InstructGPT, 2022)

| 항목 | 내용 |
|---|---|
| 저자 | Long Ouyang, Jeff Wu, Xu Jiang 외 (OpenAI) |
| 학회/저널 | NeurIPS 2022 |
| 링크 | [arXiv](https://arxiv.org/abs/2203.02155) |
| 난이도 | 🟡 |
| 사전 지식 | GPT-3 (2020), [PPO (2017)](../05-reinforcement-learning/README.md)의 개념, [DQN (2013)](../05-reinforcement-learning/2013-dqn.md) 수준의 강화학습 기초 |

## 한 줄 요약

사람이 직접 쓴 모범 답안과 "어느 답이 더 나은가"에 대한 사람의 선호를 이용해 GPT-3를 추가 학습(**RLHF**)했더니, 100배 작은 모델이 원래 GPT-3보다 사람들에게 더 좋은 평가를 받았다.

## 왜 중요한가?

**ChatGPT의 직계 조상**이 되는 논문이다. ChatGPT(2022년 11월 공개)는 이 논문과 같은 방법으로 학습되었다.

GPT-3는 인터넷 텍스트의 "다음 단어 예측"으로 학습되었기 때문에, 똑똑하지만 **사용자가 원하는 대로 행동하지는 않았다.** 질문에 답하는 대신 비슷한 질문을 더 늘어놓거나, 사실이 아닌 내용을 지어내거나, 유해한 내용을 출력하기도 했다.
이 논문은 모델을 사람의 의도에 맞추는 **정렬(alignment)** 문제를 실용적인 학습 절차로 풀어냈다. 사람 평가자들은 13억 파라미터 InstructGPT의 답변을 1,750억 파라미터 GPT-3의 답변보다 더 선호했다. **모델 크기보다 학습 방식이 더 중요할 수 있다**는 것을 보여 준 결과다.

## 핵심 아이디어

논문의 핵심 그림(3단계 학습 과정)이 전부를 요약한다.

### 1단계. 지도 파인튜닝(SFT, Supervised Fine-Tuning)

- 사람 라벨러(약 40명)가 프롬프트에 대한 **모범 답안을 직접 작성**한다
- GPT-3를 이 (프롬프트, 모범 답안) 데이터로 파인튜닝한다
- 결과: 지시를 어느 정도 따르는 SFT 모델

### 2단계. 보상 모델(RM, Reward Model) 학습

- 같은 프롬프트에 대해 SFT 모델이 만든 여러 답변(4~9개)을 라벨러가 **좋은 순서대로 순위**를 매긴다
- 답변을 입력받아 "사람이 얼마나 좋아할지"를 점수로 출력하는 보상 모델을 학습한다
- 순위 데이터는 두 답변씩 짝지어 "더 좋은 답이 더 높은 점수를 받도록" 학습한다

> 왜 모범 답안을 더 쓰지 않고 순위를 매길까? 좋은 답을 **직접 쓰는 것**보다 두 답 중 **더 나은 것을 고르는 것**이 사람에게 훨씬 쉽고 빠르기 때문이다.

### 3단계. 강화학습(PPO)으로 최적화

- SFT 모델이 프롬프트에 답을 생성하면, 보상 모델이 점수를 매긴다
- 이 점수를 **보상**으로 삼아 PPO 알고리즘으로 모델을 업데이트한다
- 단, 보상 점수만 쫓다 보면 보상 모델의 허점을 파고드는 이상한 답을 만들 수 있다. 그래서 **SFT 모델과 너무 달라지지 않도록** 벌점(KL 페널티)을 준다
- 추가로 사전학습 데이터의 학습 신호를 섞어(PPO-ptx), 기존 NLP 능력이 떨어지는 것을 줄였다

```
[사람이 쓴 모범 답안] → 1. SFT 모델
[사람이 매긴 순위]    → 2. 보상 모델
SFT 모델 + 보상 모델  → 3. PPO → InstructGPT
```

### 결과

- 사람 평가에서 InstructGPT가 GPT-3보다 크게 선호됨
- 사실을 지어내는 경우(환각)가 줄고, 유해한 출력도 약간 줄어듦
- 일부 공개 NLP 벤치마크 성능은 약간 떨어짐(논문은 이를 "**정렬 세금**", alignment tax라고 부름) → PPO-ptx로 상당 부분 완화

### 한계 (논문이 스스로 밝힘)

모델은 "인류 전체"가 아니라 **특정 라벨러 집단과 OpenAI 연구자들의 선호**에 맞춰졌다. 누구의 가치에 맞출 것인가는 여전히 열린 질문이다.

## 읽는 팁

- 본문이 길고 부록은 더 길다. 전부 읽을 필요 없다
- 먼저 읽기: 1장(서론, 주요 결과 요약)과 **3단계 학습 과정 그림**, 3.5절(모델 학습 방법: SFT, RM, RL), 4.1절 앞부분(사람 평가 결과 그래프)
- 그다음: 5장(논의), 특히 "우리는 누구에게 정렬하는가"를 다루는 절과 한계 부분
- 건너뛰어도 됨: 3.4절 라벨러 선발 과정 세부 사항, 4.2절 공개 NLP 데이터셋 평가 세부 수치, 부록 대부분
- PPO를 몰라도 "보상을 높이는 방향으로 모델을 업데이트하는 강화학습 알고리즘" 정도로 이해하면 충분히 읽을 수 있다

## 함께 보면 좋은 자료

- [Hugging Face — Illustrating Reinforcement Learning from Human Feedback (RLHF)](https://huggingface.co/blog/rlhf): RLHF 3단계를 그림으로 설명. 논문 전에 먼저 보기 좋다
- [openai/following-instructions-human-feedback](https://github.com/openai/following-instructions-human-feedback): 논문의 모델 카드와 평가용 샘플 출력

## 이어서 읽을 논문

- 이전 연구: [Deep RL from Human Preferences (2017)](https://arxiv.org/abs/1706.03741), [Learning to Summarize from Human Feedback (2020)](https://arxiv.org/abs/2009.01325): RLHF의 원형
- [Constitutional AI (2022)](https://arxiv.org/abs/2212.08073): 사람 피드백 대신 원칙 목록과 AI 피드백을 활용
- [Direct Preference Optimization (DPO, 2023)](https://arxiv.org/abs/2305.18290): 보상 모델과 강화학습 없이 선호 데이터로 직접 학습하는 더 간단한 방법
- [Llama 2 (2023)](https://arxiv.org/abs/2307.09288): 공개 모델에서 RLHF를 어떻게 했는지 자세히 공개
