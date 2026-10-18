# High-Resolution Image Synthesis with Latent Diffusion Models (Stable Diffusion, 2021)

| 항목 | 내용 |
|---|---|
| 저자 | Robin Rombach, Andreas Blattmann, Dominik Lorenz, Patrick Esser, Björn Ommer |
| 학회/저널 | CVPR 2022 |
| 링크 | [arXiv](https://arxiv.org/abs/2112.10752) |
| 난이도 | 🟡 |
| 사전 지식 | [DDPM (2020)](2020-ddpm.md), [VAE (2013)](2013-vae.md)의 오토인코더 개념, [U-Net (2015)](../02-computer-vision/2015-u-net.md), [CLIP (2021)](2021-clip.md) |

## 한 줄 요약

디퓨전을 큰 이미지의 **픽셀 공간**이 아니라 오토인코더로 압축한 작은 **잠재 공간**(latent space)에서 수행해 계산량을 크게 줄이고, **크로스 어텐션**으로 텍스트 같은 조건을 넣을 수 있게 했다. 이것이 **Stable Diffusion**의 기반이다.

## 왜 중요한가?

[DDPM](2020-ddpm.md) 같은 디퓨전 모델은 품질이 뛰어나지만, 고해상도 이미지의 모든 픽셀에 대해 수백~수천 단계를 반복해야 해서 **학습과 생성이 매우 비쌌다.** 대형 연구소만 다룰 수 있는 기술이었다.
이 논문의 잠재 디퓨전 모델(LDM)은 품질을 거의 유지하면서 비용을 크게 낮췄다. 이를 바탕으로 2022년 공개된 **Stable Diffusion**은 가중치가 공개되어 **일반 소비자용 GPU에서도** 텍스트로 이미지를 만들 수 있게 했고, 이미지 생성 AI의 대중화를 이끌었다.

## 핵심 아이디어

### 1. 두 단계로 나누기: 압축은 오토인코더가, 생성은 디퓨전이

저자들은 이미지 정보를 두 종류로 본다.

| 종류 | 예시 | 담당 |
|---|---|---|
| **지각적 세부 정보** | 미세한 질감, 픽셀 수준의 노이즈 | 오토인코더 (사람 눈에 잘 띄지 않는 정보를 압축) |
| **의미적 정보** | 무엇이 어디에 어떤 구도로 있는가 | 디퓨전 모델 (정말 중요한 내용을 생성) |

DDPM은 사람 눈에 띄지 않는 세부 정보까지 디퓨전으로 다루느라 계산을 낭비한다. 그래서:

1. **1단계**: 이미지를 작은 잠재 표현으로 압축했다가 복원하는 **오토인코더**를 먼저 학습한다. 예를 들어 512×512×3 이미지 → 64×64×4 잠재 표현(가로세로 8배 축소)
2. **2단계**: 이 **잠재 공간에서** 디퓨전 모델(U-Net)을 학습한다

생성할 때는 잠재 공간에서 노이즈를 걷어내 잠재 표현을 만든 뒤, 디코더로 한 번만 복원하면 된다.

```
텍스트 → [텍스트 인코더] ──┐ (크로스 어텐션)
                           ↓
노이즈 (64×64×4) → [U-Net으로 반복해서 노이즈 제거] → 잠재 표현 → [디코더] → 이미지 (512×512)
```

### 2. 크로스 어텐션으로 조건 넣기

"우주복을 입은 고양이" 같은 텍스트로 생성을 조종하려면 U-Net이 텍스트를 참고해야 한다.

- 텍스트를 **텍스트 인코더**(트랜스포머)로 벡터 시퀀스로 바꾼다
- U-Net 중간중간에 **크로스 어텐션** 층을 넣는다. Query는 이미지 쪽에서, Key와 Value는 텍스트 쪽에서 온다 → "이미지의 이 부분을 만들 때 텍스트의 어느 단어를 참고할까"
- 텍스트뿐 아니라 레이아웃(물체 배치도), 분할 지도, 저해상도 이미지 등 **다양한 조건**을 같은 방식으로 넣을 수 있다

### 3. 얼마나 압축할까?

압축을 너무 적게 하면(예: 2배) 계산 절약 효과가 적고, 너무 많이 하면(예: 32배) 세부 정보가 사라져 품질이 떨어진다. 실험 결과 **4~16배 축소**가 품질과 효율의 균형이 가장 좋았다.

### Stable Diffusion과의 관계

논문의 방법으로 Stability AI, Runway 등과 함께 대규모 데이터(LAION)에서 학습해 공개한 모델이 Stable Diffusion이다. 8배 압축 오토인코더, 크로스 어텐션 U-Net, CLIP 텍스트 인코더로 구성된다.

## 읽는 팁

- 먼저 읽기: 1장(서론)과 **지각적 압축 vs 의미적 압축 그래프**, 3장(방법), **구조 그림**(픽셀 공간 ↔ 잠재 공간, 크로스 어텐션 조건화. 이 그림이 Stable Diffusion 구조도 그 자체)
- 그다음: 4.1절(압축 비율에 따른 비교), 4.3절의 텍스트→이미지 생성 결과
- 건너뛰어도 됨: 오토인코더 학습의 세부 손실 함수(지각 손실 + 판별자), 초해상도·인페인팅 실험 세부 사항, 부록
- 디퓨전 자체는 이 논문에서 다시 설명하지 않으므로 DDPM 노트를 먼저 보자

## 함께 보면 좋은 자료

- [Jay Alammar — The Illustrated Stable Diffusion](https://jalammar.github.io/illustrated-stable-diffusion/): Stable Diffusion의 구성 요소를 그림으로 설명. **가장 먼저 볼 자료**
- [Hugging Face Diffusers 문서](https://huggingface.co/docs/diffusers): Stable Diffusion을 몇 줄 코드로 실행하는 라이브러리
- [CompVis/latent-diffusion](https://github.com/CompVis/latent-diffusion), [CompVis/stable-diffusion](https://github.com/CompVis/stable-diffusion): 공식 코드

## 이어서 읽을 논문

- [Classifier-Free Diffusion Guidance (2022)](https://arxiv.org/abs/2207.12598): 텍스트 조건을 더 강하게 반영하는 기법. Stable Diffusion에서 필수로 쓰임
- [SDXL (2023)](https://arxiv.org/abs/2307.01952): Stable Diffusion의 개선판
- [Scalable Diffusion Models with Transformers (DiT, 2022)](https://arxiv.org/abs/2212.09748): U-Net 대신 트랜스포머를 쓰는 디퓨전. 이후 이미지·영상 생성 모델의 주류 구조
