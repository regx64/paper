# 📚 AI 입문자를 위한 논문 모음 — 계획서

> AI를 처음 공부하는 사람이 **어떤 순서로, 어떤 논문을, 어떻게 읽으면 좋은지** 안내하는 저장소

---

## 1. 목표와 대상

**대상 독자**
- 파이썬과 고등학교~대학 1학년 수준의 수학(미분, 행렬, 확률)을 아는 사람
- 머신러닝/딥러닝 강의를 한두 개 들어봤지만 논문은 처음 읽어보는 사람

**목표**
1. 논문을 무작정 많이 모으지 않고, **입문자가 꼭 읽을 만한 30~40편**으로 범위를 정한다.
2. 논문을 **학습 순서(로드맵)** 에 맞게 배치한다. 앞 논문이 뒤 논문의 사전 지식이 되도록 한다.
3. 각 논문마다 **한국어 요약 노트**를 달아, 원문을 읽기 전에 큰 그림을 먼저 잡을 수 있게 한다.

**하지 않을 것**
- 최신 SOTA 논문 추적 (금방 낡고, 입문자에게 부담됨)
- PDF 파일 직접 업로드 (저작권 문제 → arXiv/공식 링크만 사용)

---

## 2. 저장소 구조

```
paper/
├── README.md                  # 소개, 로드맵 그림, 전체 논문 목록 표
├── HOW_TO_READ.md             # 논문 읽는 법 (3-pass 방법, 수식 대처법 등)
├── GLOSSARY.md                # 자주 나오는 용어 한국어/영어 정리
├── CONTRIBUTING.md            # 논문 추가·노트 작성 규칙
├── templates/
│   └── paper-note.md          # 논문 노트 템플릿
└── papers/
    ├── 01-foundations/        # 딥러닝 기초
    │   ├── README.md          # 이 단계의 목표와 읽는 순서
    │   └── 2015-deep-learning.md
    ├── 02-computer-vision/
    ├── 03-sequence-and-nlp/
    ├── 04-generative-models/
    ├── 05-reinforcement-learning/
    └── 06-large-language-models/
```

**파일 이름 규칙**: `연도-짧은-이름.md` (예: `2017-attention-is-all-you-need.md`)

---

## 3. 학습 로드맵과 후보 논문

난이도: 🟢 쉬움 · 🟡 보통 · 🔴 어려움  /  ⭐ = 꼭 읽기

### 단계 1. 딥러닝 기초 — "신경망은 어떻게 학습하나?"
| 논문 | 연도 | 난이도 | 비고 |
|---|---|---|---|
| ⭐ Deep Learning (LeCun, Bengio, Hinton, *Nature*) | 2015 | 🟢 | 분야 전체 개관, **첫 논문으로 추천** |
| Learning Representations by Back-propagating Errors | 1986 | 🟡 | 역전파 |
| Gradient-Based Learning Applied to Document Recognition (LeNet) | 1998 | 🟡 | CNN의 원형 |
| ⭐ Dropout | 2014 | 🟢 | 과적합 방지 |
| ⭐ Adam: A Method for Stochastic Optimization | 2014 | 🟡 | 표준 옵티마이저 |
| Batch Normalization | 2015 | 🟡 | 학습 안정화 |

### 단계 2. 컴퓨터 비전 — "이미지를 이해하는 모델"
| 논문 | 연도 | 난이도 | 비고 |
|---|---|---|---|
| ⭐ ImageNet Classification with Deep CNNs (AlexNet) | 2012 | 🟢 | 딥러닝 붐의 시작 |
| Very Deep Convolutional Networks (VGG) | 2014 | 🟢 | 단순하고 깊은 구조 |
| ⭐ Deep Residual Learning (ResNet) | 2015 | 🟡 | 잔차 연결 — 이후 모든 모델에 쓰임 |
| U-Net | 2015 | 🟡 | 분할(segmentation), 디퓨전에서도 재등장 |
| You Only Look Once (YOLO) | 2015 | 🟡 | 실시간 객체 탐지 |
| An Image is Worth 16x16 Words (ViT) | 2020 | 🟡 | 비전에 트랜스포머 적용 (단계 3 이후 권장) |

### 단계 3. 시퀀스와 자연어 처리 — "언어를 다루는 모델"
| 논문 | 연도 | 난이도 | 비고 |
|---|---|---|---|
| Long Short-Term Memory (LSTM) | 1997 | 🔴 | 원문은 어려움 → 해설 자료 위주 |
| ⭐ Efficient Estimation of Word Representations (word2vec) | 2013 | 🟢 | 단어 임베딩 |
| Sequence to Sequence Learning with Neural Networks | 2014 | 🟢 | 인코더-디코더 |
| Neural Machine Translation by Jointly Learning to Align and Translate | 2014 | 🟡 | 어텐션의 등장 |
| ⭐ Attention Is All You Need (Transformer) | 2017 | 🟡 | **가장 중요한 논문 중 하나** |
| ⭐ BERT | 2018 | 🟡 | 사전학습 + 파인튜닝 |
| Language Models are Unsupervised Multitask Learners (GPT-2) | 2019 | 🟢 | |
| Language Models are Few-Shot Learners (GPT-3) | 2020 | 🟡 | 길지만 앞부분 위주로 |

### 단계 4. 생성 모델 — "새로운 것을 만드는 모델"
| 논문 | 연도 | 난이도 | 비고 |
|---|---|---|---|
| Auto-Encoding Variational Bayes (VAE) | 2013 | 🔴 | 수식 많음 → 직관 위주 |
| ⭐ Generative Adversarial Nets (GAN) | 2014 | 🟢 | 아이디어가 직관적 |
| ⭐ Denoising Diffusion Probabilistic Models (DDPM) | 2020 | 🔴 | 이미지 생성 AI의 기반 |
| Learning Transferable Visual Models from Natural Language (CLIP) | 2021 | 🟡 | 이미지-텍스트 연결 |
| High-Resolution Image Synthesis with Latent Diffusion (Stable Diffusion) | 2021 | 🟡 | |

### 단계 5. 강화학습 — "시행착오로 배우는 모델"
| 논문 | 연도 | 난이도 | 비고 |
|---|---|---|---|
| ⭐ Playing Atari with Deep Reinforcement Learning (DQN) | 2013 | 🟡 | 딥 강화학습의 시작 |
| Mastering the Game of Go (AlphaGo) | 2016 | 🟡 | |
| Proximal Policy Optimization (PPO) | 2017 | 🔴 | RLHF에서 다시 등장 |

### 단계 6. 대규모 언어 모델(LLM) — "ChatGPT는 어떻게 만들어졌나?"
| 논문 | 연도 | 난이도 | 비고 |
|---|---|---|---|
| Scaling Laws for Neural Language Models | 2020 | 🟡 | 크기가 커지면 성능은? |
| Retrieval-Augmented Generation (RAG) | 2020 | 🟡 | 검색 + 생성 |
| ⭐ LoRA: Low-Rank Adaptation | 2021 | 🟡 | 적은 비용으로 파인튜닝 |
| ⭐ Training Language Models to Follow Instructions (InstructGPT) | 2022 | 🟡 | RLHF, ChatGPT의 직계 조상 |
| Chain-of-Thought Prompting | 2022 | 🟢 | 단계별 추론 프롬프트 |
| Training Compute-Optimal LLMs (Chinchilla) | 2022 | 🟡 | |
| LLaMA | 2023 | 🟢 | 공개 LLM의 출발점 |

> 총 **35편 내외**, 그중 ⭐ 필수 **13편**. 최종 목록은 노트를 쓰면서 조정한다.

---

## 4. 논문 노트 템플릿 (`templates/paper-note.md`)

각 논문 노트는 아래 항목을 채운다. 분량은 **A4 1~2장**이 목표.

```markdown
# 논문 제목 (연도)

| 항목 | 내용 |
|---|---|
| 저자 | |
| 학회/저널 | |
| 링크 | arXiv / 공식 PDF |
| 난이도 | 🟢/🟡/🔴 |
| 사전 지식 | 먼저 읽으면 좋은 논문 (링크) |

## 한 줄 요약
## 왜 중요한가? (이 논문 전/후로 무엇이 바뀌었나)
## 핵심 아이디어 (그림·비유로 쉽게)
## 읽는 팁 (어느 섹션부터, 무엇은 건너뛰어도 되는지)
## 함께 보면 좋은 자료 (블로그, 영상, 구현 코드)
## 이어서 읽을 논문
```

---

## 5. 진행 단계 (마일스톤)

| 단계 | 할 일 | 결과물 |
|---|---|---|
| **Phase 1. 뼈대** ✅ | 폴더 구조, README, 템플릿, CONTRIBUTING 작성 | 저장소 기본 틀 완성 |
| **Phase 2. 필수 논문** ✅ | ⭐ 13편 노트 작성 + 단계별 README | 입문 로드맵만으로 바로 활용 가능 |
| **Phase 3. 확장** ✅ | 나머지 논문 노트, `HOW_TO_READ.md`, `GLOSSARY.md` | 전체 목록 완성 |
| **Phase 4. 다듬기 (선택)** ✅ | GitHub Actions로 깨진 링크 자동 점검, 로드맵 다이어그램(Mermaid) | 유지보수 자동화 |

---

## 6. 정해야 할 것 (기본값 제안)

| 질문 | 제안 기본값 |
|---|---|
| 작성 언어 | 한국어 본문 + 논문 제목·용어는 영어 병기 |
| PDF 보관 | 하지 않음 — arXiv/공식 링크만 |
| 노트 깊이 | 입문자 눈높이의 요약 (수식 유도는 최소화) |
| 공개 범위 | 공개 저장소, 기여(PR) 환영 |
| 범위 | 2023년까지의 "고전" 위주, 최신 논문은 별도 `recent/` 폴더로 나중에 검토 |
