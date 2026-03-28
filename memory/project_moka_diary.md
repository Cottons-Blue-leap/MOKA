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
- 목소리: 차분하고 약간 낮은 여성 음성, 느긋한 템포, "귀찮은 듯 다정한" 톤 (파일럿에서 TTS 비교 후 확정 예정)

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
- Notion: https://www.notion.so/32f022ceaa59807fba76df4fa5e1d832

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

## 파일럿 영상 TODO
- [ ] LivePortrait PyTorch 2.6 호환 해결
- [ ] LoRA 학습 환경 세팅
- [ ] make_typing.py + render.bat 스크립트 제작
- [ ] TTS 음성 비교 테스트 → MOKA 목소리 확정
- [ ] 파일럿 에피소드 컷 구성 기획
- [ ] AnimateDiff 루프 테스트 (커피 김 등)
- [ ] 파일럿 영상 렌더링 + 검수
