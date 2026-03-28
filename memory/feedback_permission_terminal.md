---
name: Permission handling transparency
description: Report permission requests (type + result) to user via Discord; permissions are auto-allowed but user wants visibility
type: feedback
---

권한 관련 작업(승인, 설정 변경 등)은 디스코드가 아닌 터미널 내에서만 진행할 것.

**Why:** 사용자가 보안/관리 작업은 터미널에서 직접 컨트롤하길 원함.

**How to apply:** Permission, access, pairing 등 관리 작업이 필요할 때 디스코드로 안내하지 말고, 터미널에서 처리하도록 유도하거나 터미널에서 직접 실행할 것.

---

권한 자동 허용이 설정되어 있지만, 권한 요청이 발생할 때마다 어떤 권한인지 + 처리 결과(허용/블록)를 간략히 디스코드로 알려줄 것.

**Why:** 자동 허용을 신뢰하지만, 인간 관점에서 맥락을 파악해야 할 수 있으므로 투명성 확보가 필요.

**How to apply:** 세션 중 tool permission 요청이 발생하면 커밋 메시지처럼 간결하게 "권한: [종류] — [허용/블록]" 형태로 디스코드에 남길 것.
