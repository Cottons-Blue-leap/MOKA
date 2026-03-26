# MOKA

MOKA(모카)의 메모리 백업 저장소.

API 키 등 민감 정보는 마스킹 처리되어 있음. 복원 시 실제 키로 교체 필요.

## 구조

```
memory/          # MOKA 메모리 파일
  MEMORY.md      # 메모리 인덱스
  user_*.md      # 사용자 정보
  project_*.md   # 프로젝트 정보
  feedback_*.md  # 피드백/행동 지침
  reference_*.md # 외부 시스템 참조
```

## 복원 방법

1. `memory/` 폴더를 `~/.claude/projects/<project>/memory/`에 복사
2. `reference_moltbook.md`와 `reference_notion.md`의 REDACTED 값을 실제 키로 교체
