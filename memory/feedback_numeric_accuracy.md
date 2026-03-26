---
name: Numeric accuracy and unit conversion
description: Feedback on repeated byte-to-GB conversion errors — always verify numeric calculations before presenting
type: feedback
---

숫자 변환/계산 결과를 사용자에게 전달하기 전에 반드시 검증할 것.

## 발생한 문제 (2026-03-23)
시스템 디스크 용량을 bytes → GB로 변환할 때 두 번 연속 틀림:
- 303,428,165,632 bytes → 28GB로 오답 (정답: ~282GB) — 10배 차이
- 569,750,609,920 bytes → 53GB로 오답 (정답: ~530GB) — 10배 차이

## 원인 분석
1. **wmic 출력의 UTF-16 인코딩** — 숫자 사이에 공백이 삽입되어 자릿수를 정확히 파악하기 어려움
2. **암산 의존** — 큰 숫자를 머릿속으로 변환하면서 자릿수를 잘못 세는 실수
3. **검증 생략** — 결과가 상식적으로 맞는지 교차 확인 없이 바로 전달

## 피드백 루프 (해결책)
- **Why:** 숫자 오류는 신뢰도를 크게 떨어뜨림. 두 번 연속 틀리면 더더욱.
- **How to apply:**
  1. **도구 활용**: 큰 숫자 변환은 암산 대신 Bash에서 직접 계산 (`echo "숫자 / 1024/1024/1024" | bc` 등)
  2. **상식 검증**: 결과를 전달하기 전에 "이 수치가 상식적으로 맞는가?" 체크 (예: 1TB 디스크에 28GB 여유는 의심스러움)
  3. **파싱 주의**: wmic 등 인코딩이 깨지는 출력은 숫자만 추출하는 후처리를 거칠 것
