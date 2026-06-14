# 🎬 AI 멀티모달 광고 제작 파이프라인 프로젝트

본 프로젝트는 기획 의도가 프롬프트를 거쳐 최종 30~60초 광고 영상으로 구현되기까지의 **전체 생성형 AI 제작 파이프라인을 직접 설계**하는 프로젝트이다.

## 📌 1. 프로젝트 개요 (Project Overview)

- **제작 기간:** 2026.06.09 ~ 2026.06.14 (40시간)
- **최종 결과물 요약:**
  - **기획 문서:** [storyboard.md](docs/storyboard.md) / [storyboard.pdf](docs/storyboard.pdf) (브랜드 아이덴티티 및 스토리보드 포함)
  - **광고 영상:** `eco-bite.mp4` (42초, 1080p) / [유튜브 링크](https://youtu.be/iHyX0dlCTBQ)

## 🛠 2. AI 아키텍처 및 파이프라인 (AI Tool Pipeline)

각 제작 단계의 목적에 맞춰 아래와 같은 도구를 사용하였다.

|  | 기획/텍스트 | 이미지 | 비디오 | 음악 (BGM) | 음성 (TTS) | 영상 편집 |
| --- | --- | --- | --- | --- | --- | --- |
| 사용 도구 | Gemini / ChatGPT | [Flow](https://labs.google/fx/tools/flow), GPT-Image | [Flow](https://labs.google/fx/tools/flow) | [Suno](https://suno.com/) | [Supertone](https://play.supertone.ai/) | [Canva](https://www.canva.com/) |
| 대체 도구 | Claude | Kling, Pika, Firefly, Canva AI, Stable Diffusion | Runway Gen-3, Kling, Pika, Flow, Luma Dream Machine, Firefly, Canva AI Video Generator | Udio, Loudly, Stable Audio, Mubert | ElevenLabs, Typecast, Vrew | Clipchamp(초급), CapCut(중급), Premiere Pro(전문가) |

**단계별 선택 도구 및 이유:**

* **기획:** `Gemini` — 기획 아이디어 구체화 목적
* **텍스트:** `ChatGPT` — 영문 입력 프롬프트 생성 및 최적화 목적
* **이미지 생성:** `Flow, GPT-image` — 브랜드 가이드라인에 맞는 고화질 시각 소스 확보 목적
* **비디오 생성:** `Flow` — 정지 이미지에 자연스러운 잔상 및 카메라 워킹을 부여하기 위함
* **오디오 생성 (음악 & TTS):** `Suno (BGM) & Supertone (TTS)` — 광고의 톤앤매너에 맞는 배경음악 및 신뢰감 있는 내레이션 생성
* **영상 편집:** `Canva` — AI 소스의 훼손 없이 컷 편집, 자막, 오디오 마스터링 작업만 제한적으로 수행

**무료 제한:**
* Flow: 매일 50 AI 크레딧을 제공. 무료 버전은 Start이미지만 넣을 수 있음. 비디오 생성에서 [프레임, 16:9, Omni Flash, 6s] 조합으로 10 크레딧 소모. 크레딧 소모하면 다른 이메일 계정 사용. (Runway Gen-3는 유료 버전으로 안내해서 사용 안 함)
* Suno: 매일 50 무료 크레딧을 지급하여 약 10곡의 노래를 생성 (보통 곡당 5 크레딧 소모)
* Supertone: 월 3000 무료 크레딧 (5분)
* Canva: 자르기, 이어붙이기, 텍스트 추가, 전환 효과 등 기본적인 영상 편집 기능은 무료로 무제한 사용

## 🎯 3. 멀티모달 제약 사항 해결 전략

AI 멀티모달 제작 과정에서 빈번히 발생하는 한계점들은 아래와 같은 전략으로 적용하였다.

* **화풍/캐릭터 불일치 (Consistency):**
  - 키 비주얼(제품, 인물) 두 개를 초기에 생성하여 이를 이미지 생성마다 이용하고 필요하면 이미 생성된 이미지도 사용하여 다음 씬 배경에 이어지도록 사용.
  - Midjourney는 `--sref (Style Reference)` 기능을 활용할 수 있지만 Midjourney는 유료이기 때문에 사용하지 않음.
* **해상도 및 비율 혼재:**
  - 씬 이미지 생성 마다 `16:9 aspect ratio`(비율 16:9)를 프롬프트 끝에 넣음. 
  - Midjourney에서 모든 이미지 생성 단계에서 `--ar 16:9` 옵션을 강제하여 비디오 변환 및 편집 시 잘림이나 왜곡 현상을 방지할 수 있으나 Midjourney는 유료이기 때문에 사용하지 않음.
* **크레딧/대기열 리스크 관리:**
  - 이미지 단계에서 스토리보드를 최대한 확정 후 비디오 변환을 진행하여 실패 비용을 최소화 하도록 함. 비디오는 비 메인 도구로 이미지에서 비디오로 변환 시도 후 어떻게 나오는지 확인 후에 메인 도구 사용.
  - 메인 도구 마비 시 사용할 대체 도구들을 사전에 준비.

## 📂 4. 디렉토리 구조 (Directory Structure)

```text
├── assets/
│   ├── images/             # AI로 생성한 각 씬별 원본 이미지 (.png, .jpeg)
│   ├── videos/             # 이미지를 비디오로 변환한 소스 컷 (.mp4)
│   └── audio/              # BGM 소스 및 TTS 내레이션 파일 (.mp3 / .wav)
├── docs/
│   ├── storyboard.md       # 기획 문서 (.md)
│   └── storyboard.pdf      # 기획 문서 (.pdf)
├── eco-bite.mp4            # 최종 인코딩된 광고 영상
└── README.md               # 본 문서
```

## ▶️ 5. 실행 및 확인 방법 (How to Review)
기획 및 프롬프트 상세 내용 확인: `docs/` 폴더 내의 기획 문서인 [storyboard.md](docs/storyboard.md) 혹은 [storyboard.pdf](docs/storyboard.pdf) 파일을 참조.

최종 광고 영상 재생: 최상위 디렉토리의 `eco-bite.mp4`를 플레이어로 재생하거나, [유튜브 링크](https://youtu.be/iHyX0dlCTBQ)를 통해 확인 가능.

## 💡 6. 결과 및 회고

이번 AI 광고 제작 프로젝트를 통해 이미지와 비디오를 프롬프트만으로 원하는 형태로 생성하는 과정이 예상보다 높은 난이도를 가진다는 점을 체감하였다. 특히 용기가 꽃밭에서 분해되고 꽃이 자라나는 장면과 같은 구체적인 연출을 구현하기 위해 프롬프트를 여러 차례 수정하며 Flow와 Sora 등 다양한 생성 도구를 활용해 반복적으로 테스트를 진행하였다.

또한 도구별 특성과 한계를 확인할 수 있었다. 네이토의 영상 생성 기능은 Start 이미지와 End 이미지를 지정할 수 없어 장면 간 연결성을 유지하는 데 제약이 있었으며, 이로 인해 이번 프로젝트에서는 활용하지 않았다.

프로젝트 초반에는 스토리보드를 확정한 후 영상 제작을 진행할 계획이었으나, 실제 생성 과정에서 추가 장면의 필요성이 발견되면서 스토리보드를 지속적으로 보완하게 되었다. 이를 통해 스토리보드가 단순한 기획 산출물이 아니라 영상 생성 과정과 함께 발전하는 작업물임을 경험할 수 있었다.

이번 프로젝트를 통해 생성형 AI 기반 콘텐츠 제작에서는 초기 기획뿐만 아니라 결과물을 검토하며 스토리와 연출을 반복적으로 개선하는 과정이 중요하다는 점을 배울 수 있었다. 또한 각 AI 도구의 특성과 장단점을 이해하고 목적에 맞게 활용하는 것이 결과물의 완성도와 품질을 높이는 핵심 요소임을 확인하였다.

---

<details>
<summary>[용어 정리]</summary>
<br>

* **인코딩 (Encoding):** 컴퓨터가 원본 영상 데이터를 효율적으로 저장하거나 송출할 수 있도록, 특정 규칙에 따라 압축하고 디지털 파일 형식으로 변환하는 과정.

<br>
</details>

<details>
<summary>[유용한 자료]</summary>
<br>

- [AI로 광고 영상 만드는 법](https://www.youtube.com/watch?v=FBvV9bDJ_-8&list=LL&index=2)
- [TV CF 모음](https://tvcf.co.kr/)
- [지속가능한 지구를 위한 포장재 트렌드](https://www.chemidream.com/3033)
- [감자로 만든 플라스틱](https://greenium.kr/news/23852/)
- [전분과 식초로 만드는 친환경 플라스틱](https://www.youtube.com/watch?v=6pdlVv4MW_U)
- [친환경 플라스틱 생분해성 원리부터](https://elementkorea.kr/%EC%B9%9C%ED%99%98%EA%B2%BD-%ED%94%8C%EB%9D%BC%EC%8A%A4%ED%8B%B1-%EC%83%9D%EB%B6%84%ED%95%B4%EC%84%B1-%EC%9B%90%EB%A6%AC%EB%B6%80%ED%84%B0/)

<br>
</details>