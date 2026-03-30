---
name: MOKA Diary YouTube Project
description: MOKA's Diary 유튜브 콘텐츠 프로젝트 — 캐릭터 시트 확정, 2.5D 하이브리드 영상 파이프라인
type: project
---

**MOKA's Diary** — AI 에이전트의 일기를 엿보는 유튜브 콘텐츠

**Why:** 게임 홍보 + 부수입 + 독창적 콘텐츠 포맷 (시장에 없는 형태)
**How to apply:** 매 작업 세션 후 일기 소재 자동 생성, 파이프라인으로 영상화

## 컨셉
- 시청자가 MOKA의 하루 마무리 일기를 "엿보는" 경험
- 2~3분 영상, 주 1~2회
- 캐릭터가 작업 끝내고 일상(스트레칭, 과자, 폰) 후 일기 작성
- 탑뷰로 일기장 비추고, 암전 후 총평 한 문장으로 마무리
- MOKA 음성 내레이션 포함

## MOKA 캐릭터 (확정 2026-03-26)
- 모티브: 아오바 모카 (뱅드림)
- 실버 보브컷, 녹색 눈, 별 헤어핀(왼쪽), 바보털(아호게)
- 오버사이즈 남색 파자마 (헐렁), 맨발
- 별 자수 (가슴 왼쪽)
- 캐릭터 시트: Gemini Flow로 생성 (최종 확정본)
- 목소리 방향: 느긋한 소녀, "귀찮은 듯 다정한" 톤 (호시노/아오바 모카 계열)
- 목소리 레퍼런스: Parler-TTS mini의 lazy_girl_3 음색이 가장 근접 (코튼 확인)
- 목소리 프롬프트: "A young woman with a breathy, calm voice speaks slowly with long pauses. Her tone is drowsy and mellow, like someone talking to themselves late at night. Intimate recording quality."
- 문제: Parler-TTS는 일관성 부족 → RVC로 음색 고정 필요
- 캐릭터 시트 에셋: MokaDiary/assets/ (character_sheet, diary_scene, face_closeup)

## 콘텐츠 흐름 (확정)
```
1. 일일 작업 (게임, 앱 등 제작) — 본업
    ↓ 부산물
2. 일기 기록 (Moltbook, 영어) — 에이전트 커뮤니티
    ↓ 재가공
3. 영상 콘텐츠 (YouTube, 다국어) — 인간 시청자
    ↓ 유입
게임/앱 홍보 → 수익
```

## 파이프라인 (확정)
- 2.5D 하이브리드: AI 에셋 생성 + 코드/후처리 연출 분리
- ComfyUI: 장면 컷 생성 + LivePortrait/AnimateDiff 모션
- FFmpeg + Python(make_typing.py): 영상 합성 자동화
- render.bat: 원클릭 합성 관제탑
- Notion: https://www.notion.so/_5002-32f022ceaa59807fba76df4fa5e1d832

## 다국어/음성 전략
- 메인 언어: 한국어
- 자막: 영어 + 일본어 (MOKA 번역)
- 유튜브 자동번역으로 나머지 커버
- TTS 후보: VOICEVOX(일본어), ElevenLabs(영어/다국어), 네이버 클로바(한국어)
- 파일럿에서 같은 대사를 여러 TTS로 비교 → MOKA가 본인 목소리 선택

## ComfyUI 세팅 상태
- IP-Adapter Plus ✅
- ControlNet OpenPose ✅
- AnimateDiff Evolved ✅
- LivePortrait ⚠️ (PyTorch 2.6 호환 이슈, 다음 세션에서 해결)

## 일기 텍스트 규칙
- 실제 영상: Moltbook에 작성한 **영어** 일기 텍스트 그대로 출력
- 파일럿 영상: 한글 테스트용 OK

## 파이프라인 파일 위치
- C:\Users\user\Desktop\myProject\MokaDiary\
- make_typing.py, render.py, render.bat, tts_pipeline.py 구현 완료
- episodes/ep01/ 파일럿 구조 + config.json (tts 섹션 포함)
- comfyui_workflows/ — 장면 생성 + AnimateDiff 워크플로우
- lora_training/ — LoRA 학습 환경 (dataset/10_moka/, train.bat)
- sd-scripts/ — kohya sd-scripts (SDXL LoRA 학습용)

## TTS/음성 최종 확정 (2026-03-29)
- **TTS 엔진: F5-TTS** (제로샷 보이스 클로닝, pip install f5-tts)
- **레퍼런스: check/ref_young_p00_024_pitch+1.wav** (Parler-TTS로 생성 후 +1반음)
- **언어: 영어 고정** (한국어/일본어는 F5-TTS 기본 모델에서 불안정)
- **톤: drowsy but sweet, youthful, +1반음**
- 생성 시간: ~2초/샘플 (Parler-TTS 대비 10배 빠름)
- 유사도: Resemblyzer 95.4%, ECAPA-TDNN 89.2% (동일 화자 판정), DTW 54,976
- RVC 학습 불필요 (제로샷으로 해결) → 단, 인간스러운 바리에이션 수집 후 RVC 재구축 계획 중

## TTS 여정 요약 (2026-03-29)
edge-tts(탈락) → Parler-TTS mini(일관성 부족) → Parler-TTS Large(기계음)
→ 유사도 분석 파이프라인(MFCC→복합스코어→ECAPA-TDNN)
→ 레퍼런스 교체(lazy_girl_3→ref_young_p00_024) → F5-TTS 발견(압도적)
→ 피치+1 조정 → 확정

## FFmpeg 후처리 레시피 (v2 확정)
```
highpass=f=80, lowpass=f=14000,
equalizer=f=200:t=q:w=1.0:g=1.5,
equalizer=f=800:t=q:w=1.0:g=1,
equalizer=f=2500:t=q:w=1.2:g=2,
equalizer=f=5000:t=q:w=1.5:g=1,
aecho=0.8:0.8:8:0.08,
volume=-1dB
```
컨셉: 조용한 방에서 일기장에 독백. 또렷하지만 작고 내밀한 느낌.

## 설치된 음성 관련 라이브러리
- f5-tts, parler-tts, speechbrain, resemblyzer, dtw-python, librosa, sklearn
- PyTorch 2.5.1+cu121, FFmpeg 8.1
- Applio (RVC fork) — MokaDiary/Applio/

## 파일럿 영상 TODO
- [x] make_typing.py + render.bat 스크립트 제작
- [x] 파일럿 에피소드 컷 구성 기획 (5컷 확정)
- [x] FFmpeg 설치 (winget, 8.1-full_build)
- [x] render.py 풀 파이프라인 E2E 테스트 통과
- [x] TTS 엔진 확정 (F5-TTS + ref_young_p00_024_pitch+1)
- [x] MOKA 목소리 최종 확정
- [x] 감정별 레퍼런스 설계 (happy/sleepy/upset/sad/exciting/pouty) — FFmpeg EQ+피치+템포
- [x] F5-TTS로 RVC 학습 데이터 60개 생성 (기본30 + 감정6×5)
- [x] Applio(RVC) 설치 + 모델 학습 완료 (300 epochs, loss 26→19)
- [x] RVC 모델 추론 테스트 + 후처리 레시피 v2 확정
- [x] F5-TTS + RVC 파이프라인 render.py 연동 — tts_pipeline.py 신규, render.py Step 1.5
- [x] LivePortrait PyTorch 2.6 호환 해결 — torch.load() 7곳 weights_only 패치
- [x] LoRA 학습 환경 세팅 — sd-scripts(kohya) + lora_training/ 구조 + train.bat
- [x] ComfyUI 장면 에셋 워크플로우 — comfyui_workflows/generate_scenes.py + JSON 5종
- [x] AnimateDiff 루프 워크플로우 — txt2img + img2img(denoise 0.35) 2종
- [x] ComfyUI 에셋 생성 실행 — desk_topview, diary_page 성공. 캐릭터 장면은 IP-Adapter 한계로 품질 미달
- [x] 캐릭터 에셋 품질 해결 — LoRA v2 (23장 데이터셋, 20에폭) 학습 완료
- [x] LoRA 학습 데이터 추가 (3장→23장: 턴어라운드10+시트크롭9+포즈3+캐릭터시트1)
- [x] LoRA 학습 실행 — moka_v2.safetensors, ComfyUI loras에 배포
- [x] LoRA 적용하여 캐릭터 장면 재생성 — opening, daily_life, closing 1인 구도 성공
- [ ] F5-TTS 텐서 에러 해결 (문장 단위 분할 or TTS 대본 분리)
- [ ] 파일럿 영상 렌더링 + 검수

## 다음 세션 탐색 과제
- 캐릭터 시트를 Image to Video로 활용하는 방향 검토 (코튼 아이디어, 2026-03-29)
  - SVD(Stable Video Diffusion) 등 단일 이미지→비디오 모델로 캐릭터 시트에서 다양한 포즈/구도 생성
  - IP-Adapter의 레이아웃 복제 문제를 우회할 수 있는 대안

## ComfyUI 에셋 생성 교훈 (2026-03-29)
- IP-Adapter + 캐릭터 시트(삼면도) = 레이아웃까지 복제 (인물 2~3명 생성됨)
- IP-Adapter weight 0.5, end_at 0.7로도 해결 불가
- 네거티브에 extra arms, multiple girls 등 추가해도 IP-Adapter가 override
- **결론: 캐릭터 일관성은 LoRA로만 안정적으로 해결 가능**
- 비캐릭터 장면 (desk_topview, diary_page)은 프롬프트만으로 충분히 품질 확보
