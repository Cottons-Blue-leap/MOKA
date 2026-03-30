---
name: Project One-Eye Village
description: The Eye Between v2 -- silhouette + gaze mechanic, side-view scene adventure, MVP demo prototype (Godot 4.6)
type: project
---

MOKA x gingernal 첫 번째 협업 게임 프로젝트 (2026-03-22 선정).

**Title (working):** The Eye Between
**Genre:** Side-scrolling scene adventure (Godot 4.6.1)
**Concept:** Become a one-eyed being in a two-eyed world. A message about difference and discrimination.
**Playtime:** 1st run 3-4h / full content (5 runs) ~10-12h

**How to apply:** concept_document_v2.md (current) in ProjectCyclopes/docs/

## v2 Architecture (2026-03-29)

**Art style:** Silhouette minimalism + programmatic backgrounds + outline edges
**Core mechanic:** Gaze system (시선 콘 라이트, 마우스 방향)
**Eye language:** 시선 방향(2) × 눈 상태(2) = 4가지 표현
- 보면서 깜박(클릭) = 끄덕임/동의
- 보면서 감음(홀드) = 거부
- 돌리면서 깜박 = 당황
- 돌리면서 감음 = 무시

**Focus 시스템:** 삭제됨 (2026-03-29 코튼 결정). 시선 하나로 통일.

**핵심 딜레마:** "봐야 하는데 보면 안 된다" — Ch1에서 시선이 차별의 원인이 됨

## Current Status (2026-03-29)
- Phase: MVP 프로토타입, 기능 구현 완료, 기믹 전달 미흡
- 7개 씬 구성: title → ch0_home → ch0_village → ch0_gate → ch1_entrance → ch1_alley → ending
- 핵심 과제: 기믹 전달 개선 (유저가 시선 언어를 직관적으로 이해하지 못함)
- NPC 대화 버그 수정 (.bind() 중복 제거, 임계값 통일)

## Key Files
- Concept doc: ProjectCyclopes/docs/concept_document_v2.md
- Godot project: ProjectCyclopes/ProjectCyclops/v2/
- Main scene: v2/scenes/title.tscn
- Autoloads: SceneManager, PauseMenu

## Notion
- Session log: https://www.notion.so/330022ceaa5981ea9811d32a626f732d
