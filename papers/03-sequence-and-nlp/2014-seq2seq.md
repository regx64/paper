# Sequence to Sequence Learning with Neural Networks (2014)

| 항목 | 내용 |
|---|---|
| 저자 | Ilya Sutskever, Oriol Vinyals, Quoc V. Le (Google) |
| 학회/저널 | NeurIPS 2014 |
| 링크 | [arXiv](https://arxiv.org/abs/1409.3215) |
| 난이도 | 🟢 |
| 사전 지식 | [LSTM (1997)](1997-lstm.md), [word2vec (2013)](2013-word2vec.md) |

## 한 줄 요약

LSTM 하나(**인코더**)가 입력 문장을 읽어 고정 길이 벡터로 요약하고, 다른 LSTM(**디코더**)이 그 벡터로부터 출력 문장을 한 단어씩 만들어 내는 방식으로, 신경망만으로 기계 번역을 해냈다.

## 왜 중요한가?

입력과 출력의 길이가 서로 다르고 미리 정해져 있지 않은 문제(번역, 요약, 대화, 음성 인식)는 기존 신경망으로 다루기 어려웠다.
이 논문은 **인코더-디코더**(encoder-decoder) 구조라는 단순하고 일반적인 틀로 이 문제를 풀었다. 영어→프랑스어 번역(WMT'14)에서 수십 년간 다듬어진 통계 기반 번역 시스템과 맞먹는 성능을 냈다(BLEU 34.8, 기존 시스템 33.3).
"입력 시퀀스 → 출력 시퀀스"라는 이 틀은 [트랜스포머](2017-attention-is-all-you-need.md)에서도 그대로 이어지고, 오늘날 LLM이 "프롬프트를 읽고 답을 생성하는" 방식의 원형이다.

## 핵심 아이디어

### 1. 인코더-디코더 구조

```
인코더: A  B  C  <EOS>  →  [문장 전체를 담은 벡터 v]
디코더:                     v → W → X → Y → Z → <EOS>
```

- **인코더 LSTM**: 입력 문장을 한 단어씩 읽고, 마지막 은닉 상태를 문장 전체의 "의미 벡터"로 사용한다
- **디코더 LSTM**: 이 벡터에서 시작해 단어를 하나씩 생성한다. 방금 만든 단어를 다음 단계의 입력으로 넣는다
- 문장 끝 표시(`<EOS>`)를 생성하면 멈춘다. 그래서 출력 길이가 자유롭다

### 2. 입력 문장을 거꾸로 넣기

간단하지만 효과가 컸던 요령이다. "A B C"를 "C B A" 순서로 넣으면, 입력의 첫 단어와 출력의 첫 단어가 시간상 **가까워져서** 학습이 쉬워진다. 이것만으로 BLEU 점수가 크게 올랐다.

### 3. 빔 서치(beam search)

디코딩할 때 매 단계 가장 확률 높은 단어 하나만 고르면(탐욕적 디코딩) 앞에서의 작은 실수가 뒤까지 이어진다. 그래서 **가능성 높은 후보 문장 몇 개를 동시에 유지**하며 생성한다.

### 4. 규모

4층 LSTM, 층마다 1,000개 셀을 썼고, GPU 8장으로 약 10일 동안 학습했다.

### 한계: 병목

문장이 아무리 길어도 **고정 길이 벡터 하나**에 모든 정보를 담아야 한다. 긴 문장일수록 정보가 손실되는 이 문제를 바로 다음 논문인 [Bahdanau 어텐션](2014-bahdanau-attention.md)이 해결한다.

## 읽는 팁

- 9쪽의 짧고 읽기 쉬운 논문이다
- 먼저 읽기: 1장(서론)과 첫 그림(인코더-디코더), 2장(모델), 3.3절(입력 순서 뒤집기)
- 그다음: 3.6절 이후 결과와, 문장 벡터를 2차원으로 시각화한 그림(의미가 비슷한 문장끼리 모이고, 단어 순서가 바뀌면 다른 위치에 놓임)
- 건너뛰어도 됨: 통계 기반 번역 시스템 결과의 재채점(rescoring) 실험 세부 사항, 병렬화 설정
- 같은 시기 [Cho et al. (2014)](https://arxiv.org/abs/1406.1078)도 GRU 기반의 인코더-디코더를 독립적으로 제안했다

## 함께 보면 좋은 자료

- [Jay Alammar — Visualizing A Neural Machine Translation Model](https://jalammar.github.io/visualizing-neural-machine-translation-mechanics-of-seq2seq-models-with-attention/): Seq2Seq와 어텐션을 애니메이션으로 설명
- [PyTorch — Translation with a Sequence to Sequence Network and Attention](https://pytorch.org/tutorials/intermediate/seq2seq_translation_tutorial.html): 번역 모델 직접 구현
- [Dive into Deep Learning — Seq2Seq](https://d2l.ai/chapter_recurrent-modern/seq2seq.html)

## 이어서 읽을 논문

- [Neural Machine Translation by Jointly Learning to Align and Translate (2014)](2014-bahdanau-attention.md): 병목 문제를 해결한 어텐션
