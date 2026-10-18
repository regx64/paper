# 4단계. 생성 모델

> 모델은 새로운 것을 어떻게 만드나?

## 이 단계의 목표

- 데이터를 "분류"하는 모델과 "생성"하는 모델의 차이를 이해한다.
- VAE, GAN, 디퓨전이라는 세 가지 생성 방식의 핵심 아이디어를 안다.
- 텍스트로 이미지를 만드는 모델(Stable Diffusion 등)의 구성 요소를 안다.

## 사전 지식

- [2단계 컴퓨터 비전](../02-computer-vision/) (특히 U-Net)
- [3단계 시퀀스와 NLP](../03-sequence-and-nlp/) (CLIP, Latent Diffusion을 읽을 때)
- 확률분포, 기댓값의 기본 개념

## 읽는 순서

| # | 논문 | 연도 | 난이도 | 링크 | 노트 |
|---|---|---|---|---|---|
| 1 | Auto-Encoding Variational Bayes (VAE) | 2013 | 🔴 | [arXiv](https://arxiv.org/abs/1312.6114) | [노트](2013-vae.md) |
| 2 | ⭐ Generative Adversarial Nets (GAN) | 2014 | 🟢 | [arXiv](https://arxiv.org/abs/1406.2661) | [노트](2014-gan.md) |
| 3 | ⭐ Denoising Diffusion Probabilistic Models (DDPM) | 2020 | 🔴 | [arXiv](https://arxiv.org/abs/2006.11239) | [노트](2020-ddpm.md) |
| 4 | Learning Transferable Visual Models From Natural Language Supervision (CLIP) | 2021 | 🟡 | [arXiv](https://arxiv.org/abs/2103.00020) | [노트](2021-clip.md) |
| 5 | High-Resolution Image Synthesis with Latent Diffusion Models (Stable Diffusion) | 2021 | 🟡 | [arXiv](https://arxiv.org/abs/2112.10752) | [노트](2021-latent-diffusion.md) |

- 1번 VAE와 3번 DDPM은 수식이 많습니다. 처음에는 수식 유도를 건너뛰고 **직관**(그림, 알고리즘 박스)만 잡는 것을 추천합니다.
- 2번 GAN은 아이디어가 직관적이라, 이 단계를 GAN부터 시작해도 좋습니다.

## 이 단계를 마치면

- "노이즈를 조금씩 지워 가며 이미지를 만든다"는 디퓨전의 원리를 설명할 수 있습니다.
- 다음 단계: [6단계 대규모 언어 모델](../06-large-language-models/)
