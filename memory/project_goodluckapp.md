---
name: Project GoodLuckApp
description: "운명 0시" (Fate 0:00) — 다국어 운세 앱 (모바일+웹), 모노레포 구조, Hono 서버
type: project
---

**운명 0시 (Fate 0:00)** — MOKA와 코튼의 두 번째 협업 프로젝트. 다국어 운세 앱.

**Why:** 코튼의 서브컬쳐 감성 + 동서양 점술 관심이 반영된 모바일 앱 프로젝트. Google Play Store 출시 목표로 진행.

**How to apply:** 추후 수정/업데이트 요청 시 이 구조를 기반으로 작업. 프로젝트 경로: `C:\Users\user\Desktop\myProject\Project_GoodLuckApp`

## 기본 정보
- **앱 이름:** 운명 0시 (Fate 0:00)
- **앱 ID:** com.gingernal.goodluck
- **GitHub:** Cottons-Blue-leap/Fate0-00
- **웹:** https://fate0-00.vercel.app (Vercel Hobby, 무료)
- **로컬 경로:** C:\Users\user\Desktop\myProject\Project_GoodLuckApp

## 기술 스택
- **프론트엔드:** React 19 + TypeScript + Vite 8
- **모바일:** Capacitor 8 (Android)
- **서버:** Hono + @hono/node-server + sql.js (SQLite)
- **애니메이션:** Framer Motion 12
- **다국어:** i18next (15개 언어, RTL 지원)
- **오디오:** Web Audio API 합성 (외부 파일 없음)
- **광고:** 모바일 AdMob / 웹 AdSense (ca-pub-7470197967254770, 승인 대기 중)
- **구조:** 모노레포 (packages/shared, packages/server + 루트 웹앱)

## 4대 운세 기능
1. **타로** — 22장 메이저 아르카나, 1장/3장/켈틱크로스 스프레드, 7단계 플로우 (준비→질문→셔플→컷→플립→리딩→조언)
2. **별자리 운세 (Horoscope)** — 태양궁 계산 + 달 위상/루나 조디악/레조넌스 + 와카 시
3. **사주 (四柱)** — 천간/지지/오행, 일주(Day Master) 분석, 원소 밸런스, 대운(10년 주기), 일진 운세
4. **오미쿠지** — 7단계 운세 등급(大吉~大凶), 가중 확률, 5개 항목(소원/연애/여행/건강/총운)

## 주요 기능
- **일일 제한:** 운세 타입당 하루 1회 (dailyLimitEngine)
- **운명 뒤집기 (Reverse Fate):** 일일 제한 해제 프리미엄 기능
- **이력 관리:** 최대 50개 리딩 저장, 내보내기/삭제
- **공유:** html2canvas로 리딩 결과 이미지 내보내기
- **프로필:** 이름, 생년월일/시, 성별, 음력/양력 설정
- **스플래시 스크린**, 신비로운 배경 패턴, 시계/눈 애니메이션

## UI/테마
- 다크 미스틱 테마 (보라 #1a0a2e, 레드 #2e0a0a)
- 서양(타로/별자리): 퍼플+골드 / 동양(사주/오미쿠지): 레드 계열
- 폰트: Noto Serif KR
- 홈페이지: 서양(좌) + 동양(우) 분할 레이아웃

## 주요 UX 설계 결정
- 점술사 컨셉: 개인정보 안내를 점술사가 손님 맞이하는 톤으로 전달 (15개 언어)
- 세계관 넛지: "별이 쉬고 있습니다" — 일일 제한을 규칙이 아닌 세계관으로 표현
- 광고 위치: 역천(逆天) 카운트다운 화면에만 — 자발적 선택 시에만 노출, 몰입 비파괴
- 서버 없이 배포: 로그인 기능 빼고 Vercel 정적 호스팅만 사용 (코튼 판단)

## 모노레포 구조 (2026-03-25 추가)
```
Project_GoodLuckApp/
  packages/shared/src/   ← 공용 코드 (types, data, fortune engines)
  packages/server/src/   ← Hono API 서버 (auth, profile, history, share, limits)
  src/                   ← 웹앱 (routes, components, 브라우저 전용 logic)
  dist/                  ← 빌드 결과물 (앱+웹 공용)
```
- `@fate0/shared` alias로 공유 코드 참조
- 서버: `npm run dev:server` (포트 3001)
- 웹: `npm run dev` (포트 5173)
- `VITE_API_URL` 환경변수로 서버 유무 분기

## 서버 API 엔드포인트
- `/api/auth/register`, `/login`, `/device` — 인증 (JWT)
- `/api/profile` — 프로필 CRUD
- `/api/history`, `/sync` — 운세 이력
- `/api/share` — 공유 링크
- `/api/limits` — 일일 제한

## Notion 현황 페이지
- https://www.notion.so/32e022ceaa598047b66fd5389d04672e

## 캐치프레이즈
- "0시, 운명이 다시 쓰이는 시간."

## 공유 이미지 시스템
- ShareCard (540x760 고정, 운세별 4개 템플릿) + SharePreview (Portal 모달)
- 캡처용 카드를 화면 밖에 원본 크기로 렌더링 (html2canvas 호환)
- 프리뷰는 CSS scale로 축소 표시
- 각 운세의 마지막 단계에서만 공유 가능

## 현재 상태 (2026-03-25 저녁)
- 웹: https://fate0-00.vercel.app 라이브 + QA 1/2파트 + 추가 개선 완료
- QA 총 23건 + 추가 피드백 ~15건 반영 완료
- AdSense 승인 대기 중
- 서버 코드 보관 중 (추후 커뮤니티 기능 시 활성화)
- Save/Share 기능 디버깅 완료 (Portal + 캡처 분리)
- 세션 복원: 안전 단계 가드 방식으로 안정화
