---
name: Next.js 공식 문서 학습
description: Next.js 16 App Router 공식 문서 학습 완료 - Getting Started/Guides/API Reference 핵심
type: reference
---

# Next.js 16 (App Router) 공식 문서 학습 완료

**학습일:** 2026-03-28
**소스:** https://nextjs.org/docs
**버전:** Next.js 16.2.1

## 학습 범위

### 1. Getting Started (16개 페이지 전체)
- **Installation** — create-next-app, Turbopack 기본 번들러, Node 20.9+, TypeScript/ESLint/Tailwind 기본
- **Project Structure** — 파일 시스템 라우팅, 라우팅 파일(page/layout/loading/error/route/template/default), 메타데이터 파일, 컴포넌트 렌더링 계층
- **Layouts & Pages** — 중첩 레이아웃, 동적 세그먼트 [slug]/[...slug]/[[...slug]], searchParams, PageProps/LayoutProps 타입 헬퍼
- **Linking & Navigation** — Link 컴포넌트, 프리페칭(정적=전체/동적=부분), 스트리밍, 클라이언트 전환, useLinkStatus, window.history API 통합
- **Server & Client Components** — 기본=Server Component, 'use client' 경계, RSC Payload, 인터리빙 패턴(children slot), Context Provider 패턴, 서드파티 래핑, server-only/client-only
- **Data Fetching** — Server Component 비동기(fetch/ORM/DB), Suspense 스트리밍, loading.js, use() API, SWR/React Query, 순차/병렬 페칭, React.cache 메모이제이션
- **Mutations** — Server Functions('use server'), form action, FormData, bind로 추가 인자, useActionState, refresh(), revalidatePath/revalidateTag/updateTag, redirect, cookies
- **Caching** — 'use cache' 디렉티브, cacheLife 프로파일(seconds~max), cacheTag, PPR(Partial Prerendering), Cache Components, Suspense로 uncached 데이터 스트리밍
- **Revalidation** — 시간 기반(cacheLife), 온디맨드(revalidateTag=stale-while-revalidate, updateTag=즉시 만료, revalidatePath)
- **Error Handling** — error.js(중첩 에러 바운더리), global-error.js, not-found.js, catchError, useActionState로 expected error, unstable_retry
- **Route Handlers** — route.js, GET/POST/PUT/PATCH/DELETE/HEAD/OPTIONS, NextRequest/NextResponse, Cache Components 연동, RouteContext 타입 헬퍼
- **Metadata & OG** — static metadata 객체, generateMetadata 함수, 스트리밍 메타데이터, ImageResponse(JSX→PNG), 파일 기반(favicon/opengraph-image/robots/sitemap)
- **CSS** — Tailwind v4 + PostCSS, CSS Modules, Global CSS, 외부 스타일시트, CSS 청킹/순서
- **Images** — next/image(자동 최적화/WebP/레이지로딩/레이아웃시프트 방지), 로컬/리모트 이미지, remotePatterns 설정
- **Deploying** — Node.js 서버, Docker, Static Export, Adapter API, Verified Adapters(Vercel/Bun)

### 2. Guides (핵심 4개)
- **Authentication** — 인증 흐름(signup/login → session → authorization), Stateless/Database 세션, JWT(Jose), 쿠키 옵션(HttpOnly/Secure/SameSite), Proxy로 보호, DAL(Data Access Layer), DTO(Data Transfer Objects), 역할 기반 접근 제어, Auth Libraries 목록(NextAuth/Clerk/Supabase 등)
- **Forms** — Server Actions + form action, Zod 서버사이드 검증, useActionState 에러 표시, useFormStatus 펜딩 상태, useOptimistic 낙관적 업데이트, formAction으로 중첩 액션, requestSubmit() 프로그래밍 제출
- **Environment Variables** — .env 파일 계층(.env → .env.local → .env.development.local), NEXT_PUBLIC_ 접두사(빌드타임 인라인), 런타임 환경 변수, 변수 참조($), @next/env, 로드 순서 5단계
- **Internationalization** — locale 기반 라우팅(sub-path /fr/products), Proxy에서 Accept-Language 감지, app/[lang]/ 구조, getDictionary 패턴, generateStaticParams로 정적 생성, next-intl/lingui 등 라이브러리

### 3. API Reference (문서 구조 파악)
- **Directives:** use cache, use client, use server
- **Components:** Font, Form, Image, Link, Script
- **File Conventions:** layout/page/loading/error/route/template/default + Dynamic/Parallel/Intercepting Routes + Metadata Files
- **Functions:** 40+ (after, cacheLife, cacheTag, cookies, headers, redirect, revalidatePath, revalidateTag, updateTag, useRouter, useSearchParams 등)
- **Config:** next.config.js 70+ 옵션
- **CLI:** create-next-app, next dev/build/start

### 4. 문서 전체 구조
- App Router (메인) + Pages Router (레거시)
- Architecture (접근성, Fast Refresh, 컴파일러, 브라우저 지원)
- 총 234+ 페이지
