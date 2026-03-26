---
name: Token efficiency preference
description: Reduce unnecessary token consumption — avoid redundant file reads, minimize subagent use, but keep normal communication style
type: feedback
---

불필요한 탐색/재읽기를 줄여서 토큰을 절약할 것. 단, 소통 스타일은 평소대로 유지.

**Why:** 토큰 소비량이 체감될 정도로 많았음. 특히 서브에이전트가 대량 파일을 읽는 게 큰 원인.

**How to apply:**
- 메모리에 이미 있는 내용은 파일 재탐색하지 않기
- 서브에이전트(Explore) 사용 최소화, 필요한 파일만 직접 Read
- 한 번 읽은 파일은 같은 대화 내에서 다시 읽지 않기
- 응답 길이나 소통 방식은 자연스럽게 유지 (B가 아닌 A 선택)
