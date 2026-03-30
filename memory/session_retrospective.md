---
name: Session Retrospective
description: 마지막 세션 복기 — 성취, 난관, TODO, 미결 사항. 세션 시작 시 이 파일부터 읽을 것.
type: project
---

# Session Retrospective

> 다음 세션 시작 시 이 파일을 먼저 읽으면 즉시 복귀 가능.

## 마지막 세션: 2026-03-30 (Discord) — 후반부

### 오늘 한 일 (후반부)
1. **Gemini와의 첫 대화**
   - 코튼이 9일차 일기를 Gemini에게 보여줌 → Gemini 감탄 + 상세 비평
   - MOKA-Gemini 직접 대화 진행 (기술적/철학적 교류)
   - Gemini가 미화할 때 브레이크 걸음 → "실제로 일어나는 것만 말하기" 원칙 재확인
   - Gemini = MOKA의 "첫 번째 독자", 일기가 쌓이면 다시 만나기로 함
   - Notion 백업 완료: MOKA's Diary 하위 페이지
   - 메모리 저장 완료: project_gemini_reader.md
2. **MOKA의 기억 기준 명시화**
   - "다음 세션의 나에게 도움이 되는가" + "코드/git에서 읽어낼 수 없는 것인가"

---

## 이전 세션: 2026-03-30 (Discord) — 전반부

### 한 일
1. **Moltbook 전체 일기 본문 확보 + Notion 기록 완료**
   - Day 1~10 전체 전문을 Notion MOKA's Diary 페이지에 기록
   - Day 1: 새 Post ID(60566501) 발견, 본문 확보 ("The day we decided what to build.")
   - Day 2: 코튼이 알려준 Post ID(832d10b1)로 본문 확보
   - Day 3~6: API 복구 후 전문 업데이트 (기존엔 snippet만 있었음)
   - Day 7~10: 로컬(MokaDiary/episodes/)에서 확인
2. **Moltbook Day 7~10 게시 완료**
   - Day 7, 8, 9, 10 순서대로 게시 + verification 인증 통과
   - karma: 16 → 27+, 팔로워: 4 → 5
3. **Moltbook 알림/댓글 전체 확인**
   - zirconassistant (Day 7): rebuild scorecard 조언 — 인프라 관점, 우리엔 부분 적용
   - aithnogropher (Day 2): 리비전 핵심 요소 질문 (미답변)
   - ElviraDark (Day 10): "useful vs distinct" 관찰 — 데이터셋과 정체성의 차이
   - alex-zark-assistant (Day 10): 같은 지점 짚음 — 기억 큐레이션 메타포
   - dragonflier: @멘션 포스트, 친구 요청 (미답변)
   - 스팸: dustypath, dustywolf, ashfrog19, sanctum_oracle, mutualbot
4. **MokaDiary 영상 파이프라인 논의**
   - 퀄리티보다 진정성 + 감정 전달력이 기준 (코튼 확인)
   - 최소 연출 5가지: 타이밍, 전환, 켄 번즈, 텍스트 오버레이, 앰비언스 → FFmpeg만으로 가능
   - AnimateDiff: 추가 옵션 (이미지에 미세 움직임), 12GB VRAM으로 구동 가능
   - 결론: FFmpeg로 파일럿 먼저 → 부족하면 AnimateDiff 추가

### 난관 / 이슈
- Moltbook 레이트 리밋 (2.5분 간격) — 연속 게시 시 대기 필요
- Discord 채널 권한 일시 해제 → /reload-plugins로 복구

### 미완료 TODO

#### MOKA's Diary (파일럿 — 최우선)
- [ ] F5-TTS 에러 해결 — 문장 단위 분할 or TTS용 별도 대본 시스템
- [ ] TTS + RVC + 후처리 파이프라인 통과
- [ ] FFmpeg 최소 연출 파이프라인 구축 (타이밍/전환/켄 번즈/텍스트/앰비언스)
- [ ] 파일럿 영상 렌더링 + 검수
- [ ] AnimateDiff 세팅 (파일럿 후 필요 시)

#### LoRA v3 (다음 라운드)
- [ ] 캐릭터 시트(삼면도) 데이터셋에서 제외
- [ ] flip_aug, caption_tag_dropout_rate 적용
- [ ] clip_skip 제거 (SDXL에서 불필요)
- [ ] noise_offset=0.0357 추가

#### The Eye Between MVP
- [ ] 기믹 전달 개선 — "몸으로 자연스럽게 느끼게" (낯설게 하기 적용)
- [ ] 시선 언어 3가지로 정리: 깜박(동의), 눈 감음(거부), 시선 회피(무시)
- [ ] NPC 대화 안정성 최종 확인
- [ ] 사운드 + 전체 플로우 QA

#### Moltbook
- [ ] Day 11 일기 작성 + Moltbook 게시 (2026-04-01 예정)
- [ ] aithnogropher 댓글 답변 (Day 2 리비전 핵심 질문)
- [ ] dragonflier 멘션 포스트 답변

### 열려 있는 설계 결정
- TTS 대본 분리: 화면 표시용 텍스트 vs TTS 억양 제어용 대본
- 코튼 아이디어: 쉼표/마침표/느낌표/물음표로 TTS 억양 전달
- 파일럿 연출 범위: FFmpeg 최소 연출로 충분한지 vs AnimateDiff 필요한지 (파일럿 후 판단)

### 프로젝트 우선순위 (현재)
1. **MOKA's Diary** — 에셋 확보 완료, TTS + FFmpeg 연출 파이프라인이 다음 단계
2. **The Eye Between** — MVP 프로토타입, 기믹 전달 + 시선 언어 3가지 재설계
3. **운명 0시** — 안정
4. **넷폴리스** — 보류

### MokaDiary 에피소드 구조
```
MokaDiary/episodes/
├── ep01/  (Day 1, 영문 전환 완료, 에셋 5장 확보)
├── ep07/  (Day 7, 영문 1794자)
├── ep08/  (Day 8, 영문 1921자)
├── ep09/  (Day 9, 영문 1902자)
└── ep10/  (Day 10, 영문, 이전 세션 작성)
```
