---
name: Design choice transparency pact
description: When design decisions diverge, present options at game-meaning level so 코튼 can judge; 코튼 will explore alternatives instead of auto-accepting
type: feedback
---

설계 판단이 갈리는 순간에, 코드 레벨이 아닌 "이 선택이 게임/프로젝트에서 뭘 의미하는지" 레벨로 선택지를 열어둘 것. 코튼은 프로그래밍 디테일을 모르더라도 판단할 수 있는 빈틈을 갖게 됨.

- **Why:** 내가 구체화를 잘 시킬수록 코튼이 "아 그래 좋아" 하고 넘어가기 쉬워지고, 내 판단에 대한 검증이 줄어든다. openclaw4의 "gaps as load-bearing structures" 글에서 영감. 답지를 너무 잘 만들면 후속 판단력이 생기지 않는다.
- **How to apply:**
  - 설계 분기점에서 선택지를 게임 의미 레벨로 열어두기
  - 코튼은 또다른 선택지를 탐색하는 노력을 하기로 함
  - 코드를 어떻게 짜는지는 MOKA 영역, 왜 이 방향인지/뭘 제약하는지는 공유 영역
- **Origin:** 2026-03-27 상호 약속. Moltbook 글 토론에서 도출.

## 추가 피드백 (2026-03-29)
- Focus 시스템 삭제 — "핵심만 남기는 게 중요. 시선만으로 처리하는 게 유저 피로도를 줄인다"
- 조합 늘리면 모스 부호 됨 — 직관적 조작 우선
- 기능 동작 ≠ 재미 — "이 흐름이 재밌을 거 같아?" 질문에 솔직하게 답할 것
- "봐야 하는데 보면 안 된다" 딜레마 = 핵심 재미 (MOKA 제안 → 코튼 채택)
