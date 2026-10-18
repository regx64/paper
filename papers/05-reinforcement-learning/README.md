# 5단계. 강화학습

> 모델은 시행착오로 어떻게 배우나?

## 이 단계의 목표

- 에이전트, 환경, 보상, 정책 같은 강화학습의 기본 용어를 이해한다.
- 딥러닝과 강화학습이 결합된 방식(DQN, AlphaGo)을 안다.
- LLM 학습(RLHF)에 쓰이는 PPO가 무엇인지 감을 잡는다.

## 사전 지식

- [1단계 딥러닝 기초](../01-foundations/)
- 강화학습 기초 개념(마르코프 결정 과정, Q-러닝) — 입문 강의나 교재로 먼저 익히는 것을 추천

## 읽는 순서

| # | 논문 | 연도 | 난이도 | 링크 | 노트 |
|---|---|---|---|---|---|
| 1 | ⭐ Playing Atari with Deep Reinforcement Learning (DQN) | 2013 | 🟡 | [arXiv](https://arxiv.org/abs/1312.5602) | — |
| 2 | Mastering the Game of Go with Deep Neural Networks and Tree Search (AlphaGo) | 2016 | 🟡 | [Nature](https://www.nature.com/articles/nature16961) | — |
| 3 | Proximal Policy Optimization Algorithms (PPO) | 2017 | 🔴 | [arXiv](https://arxiv.org/abs/1707.06347) | — |

3번 PPO는 [6단계](../06-large-language-models/)의 InstructGPT(RLHF)에서 다시 등장합니다.

## 이 단계를 마치면

- 정답 레이블 없이 "보상"만으로 학습하는 방식을 설명할 수 있습니다.
- 다음 단계: [6단계 대규모 언어 모델](../06-large-language-models/)
