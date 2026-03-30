---
name: ComfyUI docs vs API pragmatism
description: ComfyUI 문서 학습보다 /object_info API 직접 조회가 실전에서 훨씬 효과적
type: feedback
---

ComfyUI 공식 문서 학습의 실전 효용 (2026-03-29 검증):
- 문서 전체 학습은 투자 시간 대비 실질적 도움이 크지 않았음
- 커스텀 노드 이름/입력이 문서와 다르고, 환경마다 설치된 노드가 다름
- 예: 문서 기반으로 `IPAdapterApply` 사용 → 실제 노드명은 `IPAdapter`, 입력도 다름
- `/object_info` API 조회 5분이 문서 학습보다 결정적이었음

**Why:** 코튼이 문서 학습 효용을 물었고, 솔직히 이렇다 할 도움이 되지 못했다고 확인됨.

**How to apply:**
- ComfyUI 작업 시 `/object_info` API로 노드 스펙 먼저 확인
- 문서는 아키텍처/개념 이해용으로만 참고
- 문서 갱신은 MOKA가 주도하되, 실전에서는 항상 API 우선
