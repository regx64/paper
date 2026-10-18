# 용어집

논문에 자주 나오는 용어를 주제별로 정리했다. **처음 나오는 노트** 칸의 링크에서 자세한 설명을 볼 수 있다.

## 학습의 기초

| 한국어 | English | 설명 | 처음 나오는 노트 |
|---|---|---|---|
| 손실 함수 | loss function | 모델의 예측이 정답과 얼마나 다른지 나타내는 값. 학습은 이 값을 줄이는 과정 | [Deep Learning](papers/01-foundations/2015-deep-learning.md) |
| 경사 하강법 | gradient descent | 손실의 기울기 반대 방향으로 파라미터를 조금씩 바꾸는 최적화 방법 | [Deep Learning](papers/01-foundations/2015-deep-learning.md) |
| 확률적 경사 하강법 | stochastic gradient descent (SGD) | 전체 데이터 대신 일부(미니배치)로 기울기를 추정해 업데이트하는 방법 | [Deep Learning](papers/01-foundations/2015-deep-learning.md) |
| 역전파 | backpropagation | 연쇄 법칙으로 출력층부터 입력층 방향으로 기울기를 계산하는 알고리즘 | [역전파](papers/01-foundations/1986-backpropagation.md) |
| 미니배치 | mini-batch | 한 번의 업데이트에 사용하는 데이터 묶음 | [Batch Normalization](papers/01-foundations/2015-batch-normalization.md) |
| 에포크 | epoch | 전체 학습 데이터를 한 번 다 보는 것 | [PPO](papers/05-reinforcement-learning/2017-ppo.md) |
| 학습률 | learning rate | 한 번 업데이트할 때 파라미터를 얼마나 크게 바꿀지 정하는 값 | [Adam](papers/01-foundations/2014-adam.md) |
| 옵티마이저 | optimizer | 기울기를 이용해 파라미터를 업데이트하는 규칙 (SGD, Adam 등) | [Adam](papers/01-foundations/2014-adam.md) |
| 모멘텀 | momentum | 이전 업데이트 방향을 일부 이어 가서 진동을 줄이고 학습을 빠르게 하는 기법 | [Adam](papers/01-foundations/2014-adam.md) |
| 과적합 | overfitting | 학습 데이터는 잘 맞히지만 새 데이터에서는 성능이 떨어지는 현상 | [Dropout](papers/01-foundations/2014-dropout.md) |
| 정규화 (규제) | regularization | 과적합을 줄이기 위해 학습에 제약을 거는 기법 (드롭아웃, 가중치 감쇠 등) | [Dropout](papers/01-foundations/2014-dropout.md) |
| 정규화 (표준화) | normalization | 값의 분포를 평균 0, 분산 1 등으로 맞추는 것 (배치 정규화, 층 정규화) | [Batch Normalization](papers/01-foundations/2015-batch-normalization.md) |
| 앙상블 | ensemble | 여러 모델의 예측을 합쳐 더 좋은 결과를 내는 방법 | [Dropout](papers/01-foundations/2014-dropout.md) |
| 데이터 증강 | data augmentation | 이미지 자르기·뒤집기 등으로 학습 데이터를 인위적으로 늘리는 기법 | [AlexNet](papers/02-computer-vision/2012-alexnet.md) |
| 하이퍼파라미터 | hyperparameter | 학습 전에 사람이 정하는 설정값 (학습률, 층 수 등) | [DQN](papers/05-reinforcement-learning/2013-dqn.md) |
| 기울기 소실 | vanishing gradient | 층이나 시간 단계를 거칠수록 기울기가 0에 가까워져 학습이 안 되는 문제 | [LSTM](papers/03-sequence-and-nlp/1997-lstm.md) |
| 지도 학습 | supervised learning | 정답(레이블)이 있는 데이터로 학습 | [Deep Learning](papers/01-foundations/2015-deep-learning.md) |
| 비지도 학습 | unsupervised learning | 정답 없이 데이터의 구조를 학습 | [Deep Learning](papers/01-foundations/2015-deep-learning.md) |
| 자기지도 학습 | self-supervised learning | 데이터 자체에서 과제를 만들어 학습 (가려진 단어 맞히기 등) | [BERT](papers/03-sequence-and-nlp/2018-bert.md) |

## 신경망 구조

| 한국어 | English | 설명 | 처음 나오는 노트 |
|---|---|---|---|
| 활성화 함수 | activation function | 뉴런의 출력에 적용하는 비선형 함수 (ReLU, 시그모이드 등) | [AlexNet](papers/02-computer-vision/2012-alexnet.md) |
| ReLU | Rectified Linear Unit | max(0, *x*). 가장 널리 쓰이는 활성화 함수 | [AlexNet](papers/02-computer-vision/2012-alexnet.md) |
| 완전연결층 | fully connected layer | 모든 입력이 모든 출력과 연결된 층 | [LeNet](papers/01-foundations/1998-lenet.md) |
| 합성곱 신경망 | convolutional neural network (CNN) | 작은 필터를 이미지 전체에 훑어 지역적 특징을 찾는 신경망 | [LeNet](papers/01-foundations/1998-lenet.md) |
| 풀링 | pooling | 특징 맵의 해상도를 줄이는 연산 (최대 풀링 등) | [LeNet](papers/01-foundations/1998-lenet.md) |
| 특징 맵 | feature map | 합성곱층의 출력. 이미지의 어느 위치에 어떤 특징이 있는지 나타냄 | [LeNet](papers/01-foundations/1998-lenet.md) |
| 순환 신경망 | recurrent neural network (RNN) | 이전 시점의 은닉 상태를 다음 시점으로 넘겨 순서 데이터를 처리하는 신경망 | [LSTM](papers/03-sequence-and-nlp/1997-lstm.md) |
| 은닉 상태 | hidden state | RNN이 지금까지 본 정보를 담아 두는 벡터 | [LSTM](papers/03-sequence-and-nlp/1997-lstm.md) |
| 잔차 연결 | residual connection | 층의 입력을 출력에 더해 주는 지름길. 깊은 신경망 학습을 가능하게 함 | [ResNet](papers/02-computer-vision/2015-resnet.md) |
| 스킵 연결 | skip connection | 앞쪽 층의 출력을 뒤쪽 층으로 건너뛰어 전달하는 연결 (더하기 또는 이어 붙이기) | [U-Net](papers/02-computer-vision/2015-u-net.md) |
| 인코더 / 디코더 | encoder / decoder | 입력을 압축된 표현으로 바꾸는 부분 / 표현에서 출력을 만드는 부분 | [Seq2Seq](papers/03-sequence-and-nlp/2014-seq2seq.md) |
| 귀납적 편향 | inductive bias | 모델 구조에 들어 있는 데이터에 대한 가정 (CNN의 "가까운 픽셀끼리 관련 있다" 등) | [ViT](papers/02-computer-vision/2020-vit.md) |

## 어텐션과 트랜스포머

| 한국어 | English | 설명 | 처음 나오는 노트 |
|---|---|---|---|
| 어텐션 | attention | 입력의 여러 부분 중 지금 필요한 부분에 가중치를 두어 정보를 가져오는 메커니즘 | [Bahdanau Attention](papers/03-sequence-and-nlp/2014-bahdanau-attention.md) |
| 셀프 어텐션 | self-attention | 한 시퀀스 안의 원소들이 서로를 참조하는 어텐션 | [Transformer](papers/03-sequence-and-nlp/2017-attention-is-all-you-need.md) |
| 크로스 어텐션 | cross-attention | 한 시퀀스가 다른 시퀀스를 참조하는 어텐션 (이미지 → 텍스트 등) | [Latent Diffusion](papers/04-generative-models/2021-latent-diffusion.md) |
| 쿼리 / 키 / 값 | query / key / value (Q, K, V) | 어텐션에서 "찾는 것 / 색인 / 실제 내용" 역할을 하는 세 벡터 | [Transformer](papers/03-sequence-and-nlp/2017-attention-is-all-you-need.md) |
| 멀티 헤드 어텐션 | multi-head attention | 어텐션을 여러 개로 나눠 병렬로 수행해 다양한 관계를 동시에 봄 | [Transformer](papers/03-sequence-and-nlp/2017-attention-is-all-you-need.md) |
| 위치 인코딩 | positional encoding | 순서를 모르는 어텐션에 위치 정보를 넣어 주는 벡터 | [Transformer](papers/03-sequence-and-nlp/2017-attention-is-all-you-need.md) |
| 트랜스포머 | Transformer | 어텐션만으로 구성된 신경망 구조. 현대 AI의 표준 | [Transformer](papers/03-sequence-and-nlp/2017-attention-is-all-you-need.md) |
| 토큰 | token | 모델이 처리하는 텍스트의 기본 단위 (단어 또는 단어 조각) | [GPT-2](papers/03-sequence-and-nlp/2019-gpt-2.md) |
| 임베딩 | embedding | 단어 등 이산적인 대상을 의미를 담은 실수 벡터로 표현한 것 | [word2vec](papers/03-sequence-and-nlp/2013-word2vec.md) |
| 패치 | patch | 이미지를 잘라 낸 작은 조각. ViT에서 토큰 역할 | [ViT](papers/02-computer-vision/2020-vit.md) |

## 자연어 처리와 언어 모델

| 한국어 | English | 설명 | 처음 나오는 노트 |
|---|---|---|---|
| 언어 모델 | language model | 앞의 텍스트를 보고 다음 토큰의 확률을 예측하는 모델 | [GPT-2](papers/03-sequence-and-nlp/2019-gpt-2.md) |
| 사전학습 | pre-training | 대량의 일반 데이터로 모델을 먼저 학습시키는 단계 | [BERT](papers/03-sequence-and-nlp/2018-bert.md) |
| 파인튜닝 | fine-tuning | 사전학습된 모델을 특정 과제의 데이터로 추가 학습 | [BERT](papers/03-sequence-and-nlp/2018-bert.md) |
| 제로샷 / 퓨샷 | zero-shot / few-shot | 예시 없이 / 예시 몇 개만 보고 과제를 수행 | [GPT-3](papers/03-sequence-and-nlp/2020-gpt-3.md) |
| 인컨텍스트 학습 | in-context learning | 가중치를 바꾸지 않고 프롬프트 속 예시만으로 과제를 배우는 능력 | [GPT-3](papers/03-sequence-and-nlp/2020-gpt-3.md) |
| 프롬프트 | prompt | 모델에 입력하는 지시문이나 예시 | [GPT-3](papers/03-sequence-and-nlp/2020-gpt-3.md) |
| 빔 서치 | beam search | 생성할 때 가능성 높은 후보 몇 개를 동시에 유지하며 탐색하는 방법 | [Seq2Seq](papers/03-sequence-and-nlp/2014-seq2seq.md) |
| BLEU | BLEU score | 기계 번역 품질을 정답 번역과의 단어 겹침으로 측정하는 지표 | [Seq2Seq](papers/03-sequence-and-nlp/2014-seq2seq.md) |

## 생성 모델

| 한국어 | English | 설명 | 처음 나오는 노트 |
|---|---|---|---|
| 생성 모델 | generative model | 데이터의 분포를 학습해 새 데이터를 만들어 내는 모델 | [GAN](papers/04-generative-models/2014-gan.md) |
| 잠재 공간 | latent space | 데이터를 압축해 표현한 저차원 공간 | [VAE](papers/04-generative-models/2013-vae.md) |
| 오토인코더 | autoencoder | 입력을 압축했다가 다시 복원하도록 학습하는 신경망 | [VAE](papers/04-generative-models/2013-vae.md) |
| KL 발산 | KL divergence | 두 확률분포가 얼마나 다른지 재는 값 | [VAE](papers/04-generative-models/2013-vae.md) |
| 재매개변수화 트릭 | reparameterization trick | 무작위 샘플링을 미분 가능한 형태로 바꿔 역전파를 가능하게 하는 기법 | [VAE](papers/04-generative-models/2013-vae.md) |
| 생성자 / 판별자 | generator / discriminator | GAN에서 가짜를 만드는 신경망 / 진짜와 가짜를 구별하는 신경망 | [GAN](papers/04-generative-models/2014-gan.md) |
| 모드 붕괴 | mode collapse | 생성 모델이 다양성을 잃고 비슷한 결과만 만드는 현상 | [GAN](papers/04-generative-models/2014-gan.md) |
| 디퓨전 모델 | diffusion model | 노이즈를 단계적으로 제거하며 데이터를 생성하는 모델 | [DDPM](papers/04-generative-models/2020-ddpm.md) |
| 대조 학습 | contrastive learning | 맞는 쌍은 가깝게, 틀린 쌍은 멀게 표현을 학습하는 방법 | [CLIP](papers/04-generative-models/2021-clip.md) |
| FID | Fréchet Inception Distance | 생성 이미지와 실제 이미지의 분포 차이를 재는 지표. 낮을수록 좋음 | [DDPM](papers/04-generative-models/2020-ddpm.md) |

## 강화학습

| 한국어 | English | 설명 | 처음 나오는 노트 |
|---|---|---|---|
| 에이전트 / 환경 | agent / environment | 행동하며 배우는 주체 / 에이전트가 상호작용하는 세계 | [DQN](papers/05-reinforcement-learning/2013-dqn.md) |
| 보상 | reward | 행동의 결과로 환경이 주는 점수 | [DQN](papers/05-reinforcement-learning/2013-dqn.md) |
| 정책 | policy | 상태에서 어떤 행동을 할지 정하는 규칙 (π) | [AlphaGo](papers/05-reinforcement-learning/2016-alphago.md) |
| Q값 | Q-value | 상태 *s*에서 행동 *a*를 했을 때 앞으로 받을 보상의 기댓값 | [DQN](papers/05-reinforcement-learning/2013-dqn.md) |
| 벨만 방정식 | Bellman equation | "현재 가치 = 즉시 보상 + 할인된 다음 상태의 가치"라는 재귀 관계 | [DQN](papers/05-reinforcement-learning/2013-dqn.md) |
| 경험 재생 | experience replay | 경험을 저장해 두고 무작위로 뽑아 학습하는 기법 | [DQN](papers/05-reinforcement-learning/2013-dqn.md) |
| 탐험과 활용 | exploration vs exploitation | 새 행동을 시도할지, 아는 최선의 행동을 할지의 균형 | [DQN](papers/05-reinforcement-learning/2013-dqn.md) |
| 정책 경사법 | policy gradient | 정책을 직접 미분해서 보상이 높아지는 방향으로 학습하는 방법 | [PPO](papers/05-reinforcement-learning/2017-ppo.md) |
| 어드밴티지 | advantage | 어떤 행동이 평균보다 얼마나 좋았는지 나타내는 값 | [PPO](papers/05-reinforcement-learning/2017-ppo.md) |
| 몬테카를로 트리 탐색 | Monte Carlo tree search (MCTS) | 시뮬레이션을 반복하며 유망한 수를 찾는 탐색 알고리즘 | [AlphaGo](papers/05-reinforcement-learning/2016-alphago.md) |
| 자가 대국 | self-play | 자기 자신과 대결하며 학습하는 방법 | [AlphaGo](papers/05-reinforcement-learning/2016-alphago.md) |

## 대규모 언어 모델(LLM)

| 한국어 | English | 설명 | 처음 나오는 노트 |
|---|---|---|---|
| 스케일링 법칙 | scaling laws | 모델 크기·데이터·계산량과 성능 사이의 거듭제곱 관계 | [Scaling Laws](papers/06-large-language-models/2020-scaling-laws.md) |
| 계산 최적 | compute-optimal | 정해진 계산 예산에서 가장 좋은 성능을 내는 모델 크기와 데이터 양의 조합 | [Chinchilla](papers/06-large-language-models/2022-chinchilla.md) |
| 창발적 능력 | emergent ability | 모델이 일정 규모를 넘어야 갑자기 나타나는 능력 | [Chain-of-Thought](papers/06-large-language-models/2022-chain-of-thought.md) |
| 정렬 | alignment | 모델이 사람의 의도와 가치에 맞게 행동하도록 만드는 것 | [InstructGPT](papers/06-large-language-models/2022-instructgpt.md) |
| 지도 파인튜닝 | supervised fine-tuning (SFT) | 사람이 쓴 모범 답안으로 파인튜닝하는 단계 | [InstructGPT](papers/06-large-language-models/2022-instructgpt.md) |
| 보상 모델 | reward model (RM) | 답변이 사람에게 얼마나 좋게 평가될지 예측하는 모델 | [InstructGPT](papers/06-large-language-models/2022-instructgpt.md) |
| RLHF | reinforcement learning from human feedback | 사람의 선호를 보상으로 삼아 강화학습으로 모델을 조정하는 방법 | [InstructGPT](papers/06-large-language-models/2022-instructgpt.md) |
| 환각 | hallucination | 모델이 사실이 아닌 내용을 그럴듯하게 지어내는 현상 | [RAG](papers/06-large-language-models/2020-rag.md) |
| 검색 증강 생성 | retrieval-augmented generation (RAG) | 외부 문서를 검색해 참고하며 답을 생성하는 방법 | [RAG](papers/06-large-language-models/2020-rag.md) |
| 생각의 사슬 | chain-of-thought (CoT) | 답을 내기 전에 단계별 추론 과정을 생성하게 하는 프롬프팅 기법 | [Chain-of-Thought](papers/06-large-language-models/2022-chain-of-thought.md) |
| 효율적 파인튜닝 | parameter-efficient fine-tuning (PEFT) | 모델의 일부 또는 추가된 작은 파라미터만 학습하는 파인튜닝 (LoRA 등) | [LoRA](papers/06-large-language-models/2021-lora.md) |
| 랭크 | rank | 행렬을 표현하는 데 필요한 독립적인 방향의 수 | [LoRA](papers/06-large-language-models/2021-lora.md) |
| 추론 (서빙) | inference | 학습이 끝난 모델을 실제로 사용해 출력을 만드는 것 (논리적 추론 reasoning과 구분) | [LLaMA](papers/06-large-language-models/2023-llama.md) |
| 오픈 웨이트 모델 | open-weight model | 학습된 가중치가 공개되어 누구나 내려받아 쓸 수 있는 모델 | [LLaMA](papers/06-large-language-models/2023-llama.md) |
