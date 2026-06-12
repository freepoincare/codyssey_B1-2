# 🎬 AI 멀티모달 광고 제작 파이프라인 프로젝트

본 프로젝트는 기획 의도가 프롬프트를 거쳐 최종 30~60초 광고 영상으로 구현되기까지의 **전체 생성형 AI 제작 파이프라인을 직접 설계**하는 프로젝트이다.

## 📌 1. 프로젝트 개요 (Project Overview)

- **제작 기간:** 2026.06.09 ~ 2026.06.13 (40시간)
- **최종 결과물 요약:**
  - **기획 문서:** `storyboard.pdf` (브랜드 아이덴티티 및 스토리보드 포함)
  - **광고 영상:** `eco-bite.mp4` ([영상 길이]초, 1080p, H.264/AAC)

## 🛠 2. AI 아키텍처 및 파이프라인 (AI Tool Pipeline)

각 제작 단계의 목적에 맞춰 아래와 같은 도구와 대체 도구를 준비하였다.

|  | 기획/텍스트 | 이미지 | 비디오 | 음악 (BGM) | 음성 (TTS) | 영상 편집 |
| --- | --- | --- | --- | --- | --- | --- |
| 사용 도구 | Gemini / ChatGPT | Flow, GPT-Image | Runway Gen-3 | Suno | Supertone | Canva |
| 대체 도구 | Claude | Kling, Pika, Firefly, Canva AI, Stable Diffusion | Kling, Pika, Firefly, Canva AI Video Generator, Flow, Luma Dream Machine | Udio, Loudly, Stable Audio, Mubert | ElevenLabs, Typecast, Vrew | Clipchamp(초급), CapCut(중급), Premiere Pro(전문가) |

**단계별 선택 도구 및 이유:**

* **기획:** `Gemini` — [기획 아이디어 구체화 목적]
* **텍스트:** `ChatGPT` — [영문 입력 프롬프트 생성 및 최적화 목적]
* **이미지 생성:** `Flow, GPT-image` — [브랜드 가이드라인에 맞는 고화질 시각 소스 확보 목적]
* **비디오 생성:** `Runway Gen-3` — [정지 이미지에 자연스러운 잔상 및 카메라 워킹을 부여하기 위함. Runway의 카메라 줌 기능 등 사용]
* **오디오 생성 (음악 & TTS):** `Suno (BGM) & Supertone (TTS)` — [광고의 톤앤매너에 맞는 배경음악 및 신뢰감 있는 내레이션 생성]
* **영상 편집:** `Canva` — [AI 소스의 훼손 없이 컷 편집, 자막, 오디오 마스터링 작업만 제한적으로 수행]

## 🎯 3. 멀티모달 제약 사항 해결 전략

AI 멀티모달 제작 과정에서 빈번히 발생하는 한계점들은 아래와 같은 전략으로 적용하였다.

* **화풍/캐릭터 불일치 (Consistency):**
  - 키 비주얼(제품, 인물) 두 개를 초기에 생성하여 이를 이미지 생성마다 이용하고 필요하면 이미 생성된 이미지도 사용하여 다음 씬 배경에 이어지도록 사용.
  - Midjourney는 `--sref (Style Reference)` 기능을 활용할 수 있지만 Midjourney는 유료이기 때문에 사용하지 않음.
* **해상도 및 비율 혼재:**
  - 씬 이미지 생성 마다 `16:9 aspect ratio`(비율 16:9)를 프롬프트 끝에 넣음. 
  - Midjourney에서 모든 이미지 생성 단계에서 `--ar 16:9` 옵션을 강제하여 비디오 변환 및 편집 시 잘림이나 왜곡 현상을 방지할 수 있으나 Midjourney는 유료이기 때문에 사용하지 않음.
* **크레딧/대기열 리스크 관리:**
  - 이미지 단계에서 스토리보드를 100% 확정 후 비디오 변환을 진행하여 실패 비용을 최소화. 비디오는 비 메인 도구로 이미지에서 비디오로 변환 시도 후 어떻게 나오는지 확인 후에 메인 도구 사용.
  - 메인 도구 마비 시 사용할 대체 도구들을 사전에 준비.

## 📂 4. 디렉토리 구조 (Directory Structure)

```text
├── assets/
│   ├── images/             # AI로 생성한 각 씬별 원본 이미지 (.png, .jpeg)
│   ├── videos/             # 이미지를 비디오로 변환한 소스 컷 (.mp4)
│   └── audio/              # BGM 소스 및 TTS 내레이션 파일 (.mp3 / .wav)
├── docs/
│   ├── storyboard.md       # 메인 기획 문서 (.md)
│   └── storyboard.pdf      # 메인 기획 문서 (.pdf)
├── eco-bite.mp4            # 최종 인코딩된 광고 영상
└── README.md               # 본 문서
```

## ▶️ 5. 실행 및 확인 방법 (How to Review)
기획 및 프롬프트 상세 내용 확인: `docs/` 폴더 내의 마크다운 기획서 혹은 제출된 PDF 파일을 참조.

최종 광고 영상 재생: 최상위 디렉토리의 `storyboard.mp4`를 플레이어로 재생하거나, [유튜브/드라이브 링크 입력]를 통해 확인 가능.

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

- AI로 광고 영상 만드는 법: https://www.youtube.com/watch?v=FBvV9bDJ_-8&list=LL&index=2
- TV CF 모음: https://tvcf.co.kr/
- 지속가능한 지구를 위한 포장재 트렌드: https://www.chemidream.com/3033
- 감자로 만든 플라스틱: https://greenium.kr/news/23852/
- 전분과 식초로 만드는 친환경 플라스틱: https://www.youtube.com/watch?v=6pdlVv4MW_U

<br>
</details>