---
name: kohya sd-scripts Documentation
description: kohya sd-scripts (LoRA/DreamBooth/Fine-tune) 공식 문서 학습 완료 — 파라미터, 데이터셋 설정, 고급 기법
type: reference
---

## 학습 범위
- GitHub: kohya-ss/sd-scripts
- 문서 5종 학습: train_network, config_README-en, sdxl_train_network, train_network_advanced, loha_lokr, validation

## 핵심 파라미터 정리

### 네트워크 아키텍처
- **LoRA**: `--network_module=networks.lora` (기본, Linear + Conv2d 1×1)
- **LoRA-C3Lier**: Conv2d 3×3 추가 — `--network_args "conv_dim=4" "conv_alpha=1"`
- **LoHa**: `networks.loha` — Hadamard product, LoRA 대비 2배 파라미터, 더 복잡한 구조 학습
- **LoKr**: `networks.lokr` — Kronecker product, 더 작은 모델 크기
- **LoRA+**: `loraplus_lr_ratio=16` — UP weights LR을 DOWN의 16배로 (논문 추천)

### 블록별 차등 설정
- `block_dims`, `block_alphas` — U-Net 블록별 개별 dim/alpha
- `conv_block_dims`, `conv_block_alphas` — Conv2d 3×3용

### SDXL 특화
- 듀얼 텍스트 인코더: `--text_encoder_lr1`, `--text_encoder_lr2` (U-Net보다 낮게, 1e-5 권장)
- `--cache_text_encoder_outputs` — VRAM 절약, 단 TE 학습 불가 → `--network_train_unet_only` 필수
- `--no_half_vae` — fp16 시 VAE 불안정 방지 (bf16은 불필요)
- `--clip_skip` — SDXL에서는 불필요/무시됨

### 옵티마이저
- AdamW8bit: 메모리 효율, bitsandbytes 필요
- Prodigy: 적응형 LR, lr=1.0 고정
- DAdaptation: 적응형
- Lion: 메모리 효율
- Adafactor: fused_backward_pass 지원

### 노이즈/정규화 기법
- `--noise_offset=0.0357` — SDXL base 기준, 밝기/대비 편향 개선
- `--adaptive_noise_scale` — latent 평균 기반 노이즈 오프셋 자동 조정
- `--multires_noise_iterations/discount` — 다해상도 노이즈, 디테일 향상
- `--min_snr_gamma` — 고노이즈 타임스텝 안정화
- `--ip_noise_gamma` — Input Perturbation 정규화
- `--debiased_estimation_loss` — Min-SNR 대안

### 손실 함수
- `--loss_type`: l1, l2(기본), huber, smooth_l1
- `--masked_loss` — 마스크 기반 부분 손실

### 데이터셋 설정 (TOML)
- `num_repeats` — 반복 횟수 (폴더명 접두사 또는 TOML)
- `shuffle_caption` — 태그 셔플
- `keep_tokens` — 앞 N개 태그 고정
- `caption_dropout_rate` — 캡션 전체 드롭 확률
- `caption_tag_dropout_rate` — 개별 태그 드롭 확률
- `flip_aug` — 좌우 반전 증강
- `color_aug` — 색상 증강
- `enable_wildcard` — 와일드카드/멀티라인 캡션

### Validation
- `--validation_split=0.1` — 데이터 10%를 검증용
- `--validate_every_n_epochs` — N에폭마다 검증
- 결과: TensorBoard `loss/validation`

### 샘플 생성
- `--sample_every_n_epochs/steps` — 학습 중 샘플 이미지 생성
- 프롬프트 파일: `--n`(네거티브), `--w/h`(크기), `--d`(시드), `--l`(CFG), `--s`(스텝)

### 학습 재개
- `--save_state` — 옵티마이저 상태 포함 저장
- `--resume` — 상태 복원 후 재개
