---
name: Project One-Eye Village
description: First collaborative game project — The Eye Between, 장면 어드벤처 (고정카메라), Florence 스타일 플랫 컬러 미니멀리즘
type: project
---

외눈박이 마을 탐방 — MOKA와 gingernal의 첫 번째 협업 게임 프로젝트 (2026-03-22 선정).

**타이틀 (가제):** The Eye Between
**장르:** 장면 어드벤처 (Godot 4.6.1)
**컨셉:** 외눈박이가 되어 쌍눈박이 세상을 탐방. 차별과 다름에 대한 메시지.
**플레이타임:** 1회차 3~4h / 5회차 전체 ~10-12h

**How to apply:** 컨셉 문서 v2.1 (concept_document_v1.md) + milestones.md + pipeline_v2_plan.md 참조.

**현재 상태:** Phase A 완료, Phase B (컨셉 아트 파이프라인) 진입 예정 (2026-03-27)
**우선순위:** The Eye Between에 집중 (2026-03-26 합의).

## 아트 스타일 전환 (2026-03-27)

**이전:** 동화 그림책 (AI 생성 완성품 → 게임 적용) — AI 느낌 제거 불가, 워크플로우 불안정
**현재:** Florence 스타일 플랫 컬러 미니멀리즘 — 캐주얼 캐릭터, 따뜻한 플랫 컬러

**Why:** AI 생성만으로는 디테일의 의도성을 확보할 수 없음. 플랫 컬러는 AI 아티팩트가 구조적으로 발생할 수 없고, 팔레트 시스템으로 톤 통일 100% 보장.

**핵심 원칙:** "AI가 구도를 잡고, 필터가 스타일을 입히고, Godot가 생명을 불어넣는다"

## 핵심 설계 결정

- **이동:** 경로 그래프 (포인트-투-포인트, Path2D 분기) — 자유이동X, 단선X
- **대면:** 선택지 + QTE (타이밍/방향/인내) — UI=세계 자체 (별도 HUD 없음)
- **Ch0 튜토리얼:** 평화로운 맥락에서 QTE 학습 (박수/술래잡기/명상)
- **해상도:** 1920×1080, 모바일 가로 고정
- **경로 원칙:** 길이 아닌 곳은 자연스러운 차단 요소(울타리/건물/수풀) 배치

## 파이프라인 v2 (플랫 컬러) — 6단계

```
① 장면 정의 (scene_config.json)
② 컨셉 아트 (generate_concept.py — 8장 러프 → 코튼 선택)
③ 배경 레퍼런스 (generate_reference.py — 확정 컨셉 기반 960×540)
④ 플랫 변환 (flatten_image.py — 엣지보존 + HSV리맵 + 대기원근 + 텍스처)
⑤ 레이어 분리 (split_layers_flat.py — far/mid/near 3레이어)
⑥ Godot 적용 (패럴랙스 + 색상그레이딩 + 파티클 + 비네트)
```

**조향 장치:** 장면별 오버라이드, 단계별 프리뷰(--preview), 부분 재처리(--from-step N)
**튜닝된 기본값:** color_count: 12, fog_strength: 0.35, remap_strength: 0.85

## 마스터 팔레트 체계

- Ch0 외눈마을: 따뜻한 계열 (H: 15~45)
- Ch1 쌍눈도시: 차가운 계열 (H: 200~240)
- 교역도시: 중립 녹색 계열 (H: 80~120)

## 구현 진행 상황

- ❌ 리소스 파이프라인 전체 삭제 (2026-03-28) — ComfyUI RnD 성과 나온 후 재개 예정
- 삭제: flatten_image.py, generate_concept.py, workflows, output, palettes, scene_configs
- 유지: docs(컨셉문서/마일스톤/파이프라인계획), Godot 코어, ComfyUI 체크포인트(Playground v2.5 포함)

## 정리 완료 (2026-03-27)

기존 AI 파이프라인 도구, AI 생성 배경, 레거시 탑다운 에셋, 전투 데이터 전부 삭제.
코어 시스템(이동/대화/대치/UI)만 유지.

## Notion

- 세션 기록: https://www.notion.so/330022ceaa5981ea9811d32a626f732d
