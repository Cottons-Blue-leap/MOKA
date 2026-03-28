---
name: ComfyUI Workflows Reference
description: ComfyUI 이론39 + Image(실전20+빌트인155+파트너44) + 3D(26) + Video(25튜+90) + Audio(6튜+51) + Utility(4튜+40) + Dev/API(8) + Hook(11) + ModelMerge(20) + FluxTutorial(7) = 전체 학습 완료
type: reference
---

ComfyUI 공식 튜토리얼 학습 (2026-03-28). docs.comfy.org

# 기초편 (development/core-concepts/) — 7개 완료

## Workflow
- 노드 네트워크 = 비주얼 프로그래밍 (Nuke/Blender/Unreal 동류)
- 저장: PNG 메타데이터 자동 내장 + JSON 독립 저장

## Nodes
- 입력→처리→출력 독립 모듈
- 4상태: Normal/Running/Error/Missing
- 3모드: Always(기본)/Never(차단)/Bypass(건너뛰기)
- 색상 코딩 9가지: Model(라벤더), CLIP(노랑), VAE(로즈), Conditioning(주황), Latent(핑크), Image(파랑), Mask(초록), Number(연두), Mesh(밝은 초록)
- 노드 그룹: 여러 노드 → 재사용 ��듈

## Custom Nodes
- 커뮤니티 확장, registry.comfy.org
- 설치: ComfyUI Manager(추천) / Git clone / ZIP 수동
- 의존성: ComfyUI 내장 Python 환경에 설치 (시스템 Python ×)
- 버전 관리: Manager UI 또는 git checkout [tag]

## Properties
- 노드 내 파라미터, 위젯(수동) ↔ 입력 포트(자동) 전환 가능
- 강타입: 호환 안 되는 타입 연결 불가

## Links
- 노드 간 데이터 흐름 선, 색상 코딩으로 타입 매칭 강제
- 표시: 커브/직각/직선/숨김
- Reroute Node로 경로 재배치

## Models
- `ComfyUI/models/` 하위: checkpoints, loras, vae, controlnet, clip, upscale_models, embeddings, clip_vision, configs
- 포맷: .safetensors, 소스: Manager/HuggingFace/CivitAI/GitHub
- extra_model_paths.yaml로 외부 경로 공유
- GGUF: 네이티브 미지원 → ComfyUI-GGUF 커스텀 노드

## Dependencies
- 4종: Assets, Custom Nodes, Python 패키지, Models
- 충돌: 버전 잠금/환경 오염/크로스 호환

# 기본편 (tutorials/basic/) — 6개 완료

## 1. Text to Image
- 6 노드: Load Checkpoint(MODEL/CLIP/VAE) → Empty Latent Image → CLIP Text Encoder(×2, pos/neg) → KSampler → VAE Decode → Save Image
- KSampler 핵심 파라미터: seed, steps, cfg, sampler_name, scheduler, denoise(t2i에선 1.0)
- 프롬프트: 영어, 쉼표 구분, 구(phrase), 가중치 `(keyword:1.2)`, 품질 키워드

## 2. Image to Image
- Text to Image에서 Empty Latent Image → **Load Image + VAE Encode** 교체
- **denoise가 핵심**: 1.0=원본 무시(=t2i), 0에 가까울수록 원본 유지
- 용도: 스타일 변환, 라인아트→포토리얼, 이미지 복원, 컬러화

## 3. Inpainting
- 마스크로 지정한 영역만 새로 생성
- **VAE Encode (for Inpainting)** 노드 사용 (mask 입력 + grow_mask_by 파라미터)
- 전용 모델(512-inpainting-ema.safetensors)이 경계 전환 더 자연스러움
- 마스크 에디터: Load Image 우클릭 → Open in MaskEditor

## 4. Outpainting
- 인페인팅의 변형 — 캔버스 확장
- **Pad Image for Outpainting** 노드가 마스크 자동 생성
- 파라미터: left/top/right/bottom(확장 px), feathering(전환 부드러움)
- 출력(image+mask) → VAE Encode (for Inpainting)에 연결

## 5. Upscale
- 가장 심플: Load Image → Upscale Image (Using Model) → Save Image
- 모델 경로: `ComfyUI/models/upscale_models/`
- 모델별 특성: RealESRGAN(범용), BSRGAN(텍스트/엣지), SwinIR(자연 텍스처)
- 고급: 체인 업스케일(2x→4x), 하이브리드(t2i→upscale)
- 모델 다운로드: OpenModelDB

## 6. LoRA / Multiple LoRAs
- Low-Rank Adaptation: 베이스 모델 수정 없이 스타일 주입
- Load LoRA 노드: lora_name, strength_model(UNet 영향), strength_clip(텍스트 영향)
- 파일 경로: `ComfyUI/models/loras/`
- 체인 연결: Load LoRA → Load LoRA → ... (순서 중요, strength로 밸런싱)
- 변형: Lycoris, loha, lokr, locon

# ControlNet편 (controlnet/) — 5개 완료

## 7. ControlNet 기본
- 텍스트만으론 불가능한 구조/포즈/구도 정밀 제어
- Load ControlNet + Apply ControlNet 노드 추가
- Apply ControlNet: strength, start_percent, end_percent
- conditioning에 끼어듦 → 체인 연결 가능, LoRA와 동시 사용 가능
- 전처리 필요: 타입별(scribble, depth, openpose, canny) 참조 이미지 변환
- 커스텀 노드: ComfyUI ControlNet aux, ComfyUI-Advanced-ControlNet

## 8. Pose ControlNet + 2-Pass
- OpenPose: 몸 18 + 얼굴 70 + 손 21 + 발 6 키포인트
- 2-Pass: Pass 1(모델A, denoise 1.0, 구조+포즈) → Upscale Latent → Pass 2(모델B, denoise 0.4~0.6, 스타일 정제)
- 장점: 고해상도, 스타일 블렌딩, GPU 효율

## 9. Depth ControlNet
- 깊이맵(그레이스케일, 밝=가까움, 어두움=멀음)으로 3D 공간 구조 제어
- 용도: 인물-배경 관계, 풍경 레이어, 건축 원근, 제품 배경 분리
- 조합: Depth+Lineart, Depth+Pose

## 10. T2I Adapter (경량 대안)
- Tencent ARC Lab, ~77M(~300MB), ControlNet 대비 약 3배 빠름
- 워크플로우 동일(Apply ControlNet 노드), 모델 파일만 교체
- 5가지 타입: Depth, Line Art, Keypose, Segmentation, Color
- 다중 조건 조합 시 ControlNet보다 효율적

## 11. Mixing ControlNets
- Apply ControlNet 체인으로 다중 ControlNet 동시 적용
- 영역 분할(좌/우 별도 제어) 또는 다차원 제어(같은 피사체에 Pose+Depth)
- strength 밸런싱 중요 — 비슷하게 맞추기
- 프롬프트에 모든 제어 영역 요소 포함 필수

# Interface편 (interface/) — 7개 완료

## Overview
- UI 5영역: 상단 네비, 왼쪽 사이드바(Assets/Nodes/Models/Workflows/Templates), 오른쪽 패널, 좌하단 툴바, 우하단 캔버스
- 6개 언어 (한국어 포함), `r`키로 모델 새로고침

## APP Mode
- 노드 그래프 숨기고 입력/출력만 노출하는 간소화 인터페이스
- 4단계: 입력 선택 → 출력 선택 → 미리보기 → 기본 뷰 설정

## Nodes 2.0
- LiteGraph Canvas → Vue 기반 전환, 토글 가능

## Mask Editor
- 내장 마스크 편집기, Load Image 우클릭 → Open in MaskEditor

## Workflow Templates
- `Workflow` → `Browse Workflow Templates`, Load→Download→Execute
- HuggingFace/CivitAI만 인식, .safetensors만 허용

## Subgraph
- 노드 그룹 → 하나의 재사용 노드, 네스팅/언패킹/Blueprint 발행

## Partial Execution
- 출력 노드까지의 경로만 실행 (녹색 삼각형), v1.24.x+

# Settings편 (interface/settings/) — 13개 완료

## Overview — Ctrl+, 접근, comfy.settings.json 자동 저장, 12개 카테고리
## User — 계정/인증, API 노드용, 4가지 로그인(Email/Google/GitHub/API Key), localhost만
## Credits — API 노드용 크레딧, 로컬은 무료, Stripe 결제, 환불 불가, 충전 1년 만료
## Comfy — 핵심 설정: 자동 저장, 누락 경고, Dev 모드, 토큰 가중치(Ctrl+↑↓, 0.01), 노드 검색
## LiteGraph — 캔버스: 줌 속도(1.1), 그리드 스냅(10px), 링크 스타일(Spline기본), FPS, 저품질 렌더링 임계값
## Appearance — 컬러 팔레트(JSON 테마) + user.css, 노드 투명도, 사이드바 위치/스타일
## 3D — 카메라(Perspective/Ortho), 조명(강도1~10), 씬(배경/그리드) — 당분간 불필요
## Comfy Desktop — Desktop 전용, 윈도우 스타일, 업데이트, 미러 — Portable은 해당 없음
## Mask Editor — 브러시 속도 배수, 주축 잠금, 새 에디터 권장
## Keybinding — 단축키 커스터마이즈, 4카테고리(워크플로우/노드/인터페이스/검색)
## Extension — 프론트엔드 UI 확장 관리 (Custom Nodes=백엔드와 별개), 새로고침 필요
## About — 버전 뱃지 4개, 시스템 통계
## Server Config — 서버/GPU/메모리: 정밀도(UNET/VAE/텍스트 FP64~FP8), VRAM 전략(Auto~CPU), 프리뷰, 캐싱, xFormers

# Image Built-in 노드 레퍼런스 — ~155개 완료 (2026-03-28)
## 21개 카테고리: Image로드저장(12), 리사이즈(8), 크롭변형(6), 합성블렌딩(6), 필터조정(12), 채널색공간(8), 배치(7), 유틸(4), Mask(9), Latent(25+), VAE(6), Sampling(9), Conditioning(13), Model로더(4), CLIP(6), LoRA(2), ControlNet(7), Style/Vision(4), 업스케일(2), Model패치(3)
## 상세 레퍼런스: comfyui_builtin_nodes_image_reference.md (로컬 파일)
## 미학습 튜토리얼: utility/preprocessors, utility/image-upscale, utility/frame-interpolation, flux/ 전용 7개

# 실전편 — Image

## Flux 패밀리 (8개)
- Flux.2 Dev: 차세대, Mistral 인코더, 멀티레퍼(10장), 4MP, 오픈소스
- Flux.2 Klein 4B: 최속(1.2초 RTX5090), t2i+편집 통합, Base/Distilled
- Flux.1 Krea Dev: AI느낌 없는 미학, DualCLIP(CLIP-L+T5-XXL), 비상업
- Flux.1 Kontext Dev: 텍스트+이미지 편집, 12B, "Change X to Y, keep Z unchanged"
- Flux.1 Dev/Schnell: 기본 T2I, Schnell=Apache2.0/4스텝/저사양
- USO (ByteDance): 스타일+주체 분리(Subject/Style/Combined/T2I), LoRA+CLIP Vision
- Flux.1 Fill Dev: Inpaint/Outpaint 전용, 상업OK
- Flux.1 ControlNet: Canny/Depth, 풀모델 or LoRA버전, 커뮤니티(InstantX/XLab)
- 상업OK: Schnell, Fill Dev, Flux.2 Dev / 비상업: Flux.1 Dev, Krea

## Qwen 패밀리 (5개) — 전부 Apache 2.0
- Qwen-Image: 20B MMDiT, 다국어 텍스트(한/중/일/영), 텍스트인코더=Qwen2.5VL7B
- Qwen-Image-2512: 12월 업데이트, 인물리얼리즘/디테일 향상, 7종횡비, Lightning4스텝
- Qwen-Image-Edit: 편집전용, 듀얼모드(시맨틱+외관), 다국어텍스트편집
- Qwen-Image-Edit-2511: 11월업데이트, ImageDrift완화, 캐릭터보존강화, BF16
- Qwen-Image-Layered: ⭐ RGBA레이어 자동분해, 재귀분해, 전용VAE, 외눈마을패럴랙스핵심
- 권장: 생성=2512, 편집=2511, 레이어=Layered

## Z-Image (2개) — 알리바바 Tongyi Lab
- Z-Image: 6B Single-Stream DiT, Qwen3 4B 인코더, 중/영텍스트, 프롬프트인핸서
- Z-Image-Turbo: 증류 8NFE 서브초, 16GB OK, Fun Union ControlNet
- 패밀리: Base(파인튜닝)/Turbo(고속)/Edit(편집)

## HiDream (2개) — 전부 MIT
- I1: 17B DiT+MoE, 4중인코더(CLIP×2+T5+Llama), Full(50)/Dev(28)/Fast(16)스텝, FP8~16GB
- E1/E1.1: 편집전용, E1.1권장(동적1MP), 34.2GB, VRAM매우높음

## Ovis (1개) — 7B 텍스트렌더링 특화, 20B급 품질, 중/영, 포스터/로고/UI목업

## NewBie (1개) — 3.5B 애니메이션특화, XML구조프롬프트(캐릭터별 속성분리), Gemma3+JinaCLIP

## Cosmos Predict2 (1개) — NVIDIA 물리세계모델, 물리시뮬레이션/환경상호작용, T2I+Video2World

## OmniGen2 (1개) — 7B(3B텍스트+4B이미지) 독립경로, Qwen2.5VL인코더, T2I+편집통합

## VAE 공유: 대부분 Flux VAE(ae.safetensors) 공유. 예외: Qwen전용VAE, Qwen-Layered전용VAE
## 라이선스: MIT(HiDream) / Apache2.0(Qwen,Schnell) / 상업OK(Flux.2Dev,FillDev) / 비상업(Flux.1Dev,Krea)

## 워크플로우 템플릿 위치
`C:\Users\user\Desktop\myProject\ComfyUI_windows_portable\ComfyUI\user\default\workflows\`
- Text to Image 관련 47개 (로컬 27 + API 20)

## 프로젝트별 우선순위 (1~4순위 + 불필요)
1순위: Text to Image, Character Reference, Image to Image, Style Reference, Style Transfer, ControlNet, Inpainting
2순위: Layer Decompose, Image to Video, Upscale, Image Edit, Outpainting
3순위: Video to Video, Video Editing, Text to Audio, Audio, Character
4순위: Anime, Layout Design, Portrait, Text to Video 등
학습완료: 3D (26노드: Load/Preview4 + Hunyuan3D3 + Tripo8 + Meshy7 + Rodin5)
학습완료: Video (25튜토리얼 + ~90노드) — Wan2.1/2.2, Hunyuan, LTX, Cosmos, Kandinsky, 파트너API
  상세 레퍼런스: comfyui_video_reference.md (로컬 파일)
학습완료: Audio (6튜토리얼 + 51노드) — ACE-Step v1/1.5, Stable Audio, ElevenLabs, LTXV AV, Wan S2V, Kling
  상세 레퍼런스: comfyui_audio_reference.md (로컬 파일)
학습완료: Utility (4튜토리얼 + ~40노드) — 전처리기, 업스케일, 보간, Primitive/String/Regex/Flow/Batch
  상세 레퍼런스: C:\tmp\comfyui_utility_research.md
불필요: Fashion, Product, Vector 등

# Partner Image/Enhancement 노드 — 44개 신규 (2026-03-29)
학습완료: BFL(2), Ideogram(3), Recraft(15), StabilityAI Image(2), OpenAI Image+Chat(5),
  Luma Image(3), Google Gemini/Image(5), Magnific/Freepik(5), WaveSpeed(2),
  Reve(3), Bria Edit(2), ByteDance Image(4), Runway Image(1), Grok Image(2), Pika Scenes(1)
  상세 레퍼런스: comfyui_partner_image_reference.md (로컬 파일)
가격 최저가: Recraft 0.21/run, Luma Flash 0.57, WaveSpeed SeedVR2 2.11
핵심 활용: Recraft(벡터SVG+최저가), Luma(포토리얼+참조), Ideogram(텍스트렌더링),
  BFL Kontext(이미지편집), Magnific(업스케일+리라이팅), GPT-Image-1(투명배경)

# Development / API — 8개 영역 완료 (2026-03-29)
## Server Architecture: aiohttp+asyncio 기반, REST(api.fetchApi)+WebSocket(send_sync)
## REST API Routes: 24개 (/, /ws, /prompt, /queue, /history, /interrupt, /system_stats, /free, /upload/image, /upload/mask, /object_info, /embeddings, /models, /view, /extensions, /features, /users, /userdata 등)
## WebSocket Messages: 9종 (execution_start/error/interrupted/cached/success, executing, executed, progress, status)
## 커스텀 메시지: 서버=PromptServer.instance.send_sync(), 클라이언트=api.addEventListener()
## API Key: extra_data.api_key_comfy_org로 headless 유료 노드 접근
## Cloud API: https://cloud.comfy.org, X-API-Key 헤더, /api/job/{id}/status 또는 WSS 폴링
## Execution Model: PR#2666 front-to-back 위상정렬 전환, Lazy Eval, Node Expansion
## Custom Node 개발:
  - 4유형: Server-only(주), Client-only, Independent, Connected
  - 필수: CATEGORY, INPUT_TYPES(@classmethod), RETURN_TYPES, FUNCTION
  - 선택: RETURN_NAMES, OUTPUT_NODE, IS_CHANGED, VALIDATE_INPUTS, SEARCH_ALIASES
  - 등록: NODE_CLASS_MAPPINGS, NODE_DISPLAY_NAME_MAPPINGS, WEB_DIRECTORY
  - 데이터: IMAGE[B,H,W,C], MASK[B,H,W], LATENT{samples:[B,C,H,W]}, AUDIO{waveform+sample_rate}
  - 고급: lazy eval(lazy:True+check_lazy_status), ExecutionBlocker, Node Expansion(GraphBuilder), LIST(OUTPUT_IS_LIST/INPUT_IS_LIST)
  - Migration: NodeReplace API (old->new 매핑)
  상세 레퍼런스: C:\tmp\comfyui_remaining_research.md (Section 1)

# Hook System Nodes — 11개 완료 (2026-03-29)
## 용도: 샘플링 특정 타임스텝에서 LoRA/모델 패치 동적 적용 + 키프레임 스케줄링
## Combine: CombineHooks(2), CombineHooksFour(4), CombineHooksEight(8) — HOOKS 병합
## Create Keyframe: CreateHookKeyframe, CreateHookKeyframesFromFloats, CreateHookKeyframesInterpolated
  - strength_mult/start_percent/end_percent로 시간축 강도 제어
## Create LoRA Hook: CreateHookLora(모델+CLIP), CreateHookLoraModelOnly, CreateHookModelAsLora(체크포인트->LoRA), CreateHookModelAsLoraModelOnly
  - strength_model/strength_clip -20~20, lora_name 또는 ckpt_name
## Apply: SetHookKeyframes(훅+키프레임), SetClipHooks(CLIP에 훅), SetModelHooksOnCond(conditioning에 훅)
## 패턴: CreateHookLora -> SetHookKeyframes -> SetClipHooks/SetModelHooksOnCond
  상세 레퍼런스: C:\tmp\comfyui_remaining_research.md (Section 2)

# ModelMerge Nodes — 20개 완료 (2026-03-29)
## 기본 4개: Simple(ratio), Add(패치추가), Subtract(multiplier), Blocks(input/middle/out 3-zone)
## 아키텍처별 16개: SD1(30블록), SDXL(25), SD3_2B(30), SD35_Large(44), Flux1(63), WAN2_1(~46), Cosmos7B(35), Cosmos14B(42), CosmosPredict2_2B(34), CosmosPredict2_14B(41), LTXV(32), MochiPreview(53), QwenImage(63), Auraflow(41)
## 공통: model1+model2 입력, 각 블록 FLOAT 0.0~1.0 (0=model2 기여없음, 1=model2 전체)
  상세 레퍼런스: C:\tmp\comfyui_remaining_research.md (Section 3)

# Flux Tutorials — 7개 완료 (2026-03-29)
## Flux.1 T2I: Dev(비상업)/Schnell(Apache,4step)/Pro(API), FP8 간소화 지원, 네거티브 프롬프트 불필요
## Flux.1 Fill Dev: Inpaint+Outpaint 전용, flux1-fill-dev.safetensors
## Flux.1 Kontext Dev: 12B 멀티모달 편집, "Change X to Y, keep Z unchanged" 패턴, 영어전용
## Flux.1 ControlNet: Canny풀모델/Depth LoRA 2워크플로우, 커뮤니티(InstantX/XLab)
## Flux.1 USO: ByteDance, Subject/Style/Combined/T2I 4모드, LoRA+CLIP Vision+ModelPatch
## Flux.2 Dev: Mistral인코더, flux2-vae, 멀티레퍼(10장), 4MP, Flux.1과 비호환
## Flux.2 Klein: 최속(4B Distilled 1.2초), Qwen3 인코더, t2i+편집 통합, 4B/9B
  상세 레퍼런스: C:\tmp\comfyui_remaining_research.md (Section 4)
