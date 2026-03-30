---
name: PyTorch Documentation Reference
description: PyTorch 2.11 공식 문서 학습 — Core(Tensor/nn/autograd/optim), CUDA, AMP, Data, Serialization, Compile
type: reference
---

# PyTorch 2.11 공식 문서 학습

**학습일:** 2026-03-29
**소스:** https://docs.pytorch.org/docs/stable/
**설치 버전:** PyTorch 2.5.1+cu121 (로컬)

## 학습 범위

### 1. torch (Core Module)

#### 텐서 생성
- 기본: `tensor()`, `zeros()`, `ones()`, `empty()`, `full()`, `eye()`
- 시퀀스: `arange()`, `linspace()`, `logspace()`
- Like 변형: `zeros_like()`, `ones_like()`, `empty_like()`, `full_like()`, `rand_like()`, `randn_like()`
- 외부 데이터: `from_numpy()`, `as_tensor()`, `asarray()`, `frombuffer()`
- 스파스: `sparse_coo_tensor()`, `sparse_csr_tensor()` 등

#### 텐서 조작
- 변형: `reshape()`, `view()`, `squeeze()`, `unsqueeze()`, `flatten()`, `unflatten()`
- 차원: `transpose()`, `permute()`, `movedim()`, `t()`
- 결합/분리: `cat()`, `stack()`, `split()`, `chunk()`, `hstack()`, `vstack()`
- 선택: `select()`, `index_select()`, `masked_select()`, `gather()`, `where()`
- 산포: `scatter()`, `scatter_add()`, `scatter_reduce()`

#### 수학 연산
- 산술: `add()`, `sub()`, `mul()`, `div()`, `pow()`, `remainder()`
- 삼각함수: `sin()`, `cos()`, `tan()`, `asin()`, `acos()`, `atan()`, `atan2()`
- 지수/로그: `exp()`, `log()`, `log2()`, `log10()`, `sqrt()`, `rsqrt()`
- 특수: `erf()`, `erfc()`, `sigmoid()`, `softmax()`, `clamp()`
- 리덕션: `sum()`, `mean()`, `std()`, `var()`, `min()`, `max()`, `argmin()`, `argmax()`, `prod()`, `median()`
- 비교: `eq()`, `ne()`, `lt()`, `le()`, `gt()`, `ge()`, `allclose()`, `isnan()`, `isinf()`
- 선형대수: `matmul()`, `mm()`, `bmm()`, `mv()`, `dot()`, `outer()`, `inverse()`, `det()`, `svd()`, `qr()`
- 비트: `bitwise_and()`, `bitwise_or()`, `bitwise_xor()`, `bitwise_not()`

#### 랜덤
- 생성: `rand()`, `randn()`, `randint()`, `randperm()`, `normal()`, `bernoulli()`, `multinomial()`
- 시드: `manual_seed()`, `seed()`, `get_rng_state()`, `set_rng_state()`

#### 직렬화
- `save()`, `load()` — ZIP64 포맷, `.pt`/`.pth` 확장자
- `weights_only=True` (PyTorch 2.6+ 기본값) — 보안 강화, state_dict만 안전하게 로드
- 뷰 관계 보존 (작은 텐서가 큰 스토리지의 뷰면 전체 저장 → `.clone()` 필요)
- `add_safe_globals()`, `safe_globals()` — unsafe global 허용 리스트

#### 그래디언트 제어
- `no_grad()`, `enable_grad()`, `set_grad_enabled()`, `inference_mode()`

### 2. torch.nn

#### 컨테이너
- `Module` (베이스), `Sequential`, `ModuleList`, `ModuleDict`, `ParameterList`, `ParameterDict`

#### 레이어
- **Linear**: `Linear`, `Bilinear`, `Identity`, `LazyLinear`
- **Conv**: `Conv1d/2d/3d`, `ConvTranspose1d/2d/3d`, `Unfold`, `Fold`
- **Pooling**: `MaxPool1d/2d/3d`, `AvgPool1d/2d/3d`, `AdaptiveMaxPool/AvgPool`, `FractionalMaxPool`
- **Padding**: `ReflectionPad`, `ReplicationPad`, `ZeroPad`, `ConstantPad`, `CircularPad` (1d/2d/3d)
- **Normalization**: `BatchNorm1d/2d/3d`, `GroupNorm`, `LayerNorm`, `InstanceNorm1d/2d/3d`, `RMSNorm`, `SyncBatchNorm`
- **Recurrent**: `RNN`, `LSTM`, `GRU`, `RNNCell`, `LSTMCell`, `GRUCell`
- **Transformer**: `Transformer`, `TransformerEncoder/Decoder`, `TransformerEncoderLayer/DecoderLayer`
- **Dropout**: `Dropout`, `Dropout1d/2d/3d`, `AlphaDropout`
- **Embedding**: `Embedding`, `EmbeddingBag`
- **Upsampling**: `Upsample`, `PixelShuffle/Unshuffle`, `ChannelShuffle`

#### 활성화 함수
- ReLU계열: `ReLU`, `ReLU6`, `LeakyReLU`, `PReLU`, `RReLU`, `ELU`, `SELU`, `CELU`
- 시그모이드계열: `Sigmoid`, `Tanh`, `Hardswish`, `Hardsigmoid`, `Hardtanh`
- 현대적: `GELU`, `Mish`, `SiLU(=Swish)`, `GLU`
- Softmax계열: `Softmax`, `LogSoftmax`, `Softmin`
- 기타: `Threshold`, `Softsign`, `Softshrink`, `Hardshrink`, `LogSigmoid`
- **MultiheadAttention** — 어텐션 메커니즘

#### 손실 함수
- 회귀: `L1Loss(MAE)`, `MSELoss`, `SmoothL1Loss(Huber)`, `HuberLoss`
- 분류: `CrossEntropyLoss`, `NLLLoss`, `BCELoss`, `BCEWithLogitsLoss`
- 분포: `KLDivLoss`, `PoissonNLLLoss`, `GaussianNLLLoss`
- 랭킹: `MarginRankingLoss`, `TripletMarginLoss`, `CosineEmbeddingLoss`, `MultiMarginLoss`
- 특수: `CTCLoss`, `AdaptiveLogSoftmaxWithLoss`

#### 유틸리티
- `clip_grad_norm_()`, `clip_grad_value_()` — 그래디언트 클리핑
- `parameters_to_vector()`, `vector_to_parameters()`
- `weight_norm()`, `spectral_norm()`
- `Parameter`, `Buffer` — 학습 가능/불가능 텐서 래퍼

### 3. torch.autograd

#### 핵심 개념
- **역전파 자동미분 (Reverse-mode AD)** — 순방향 실행 중 DAG 구성, backward()로 역추적
- **동적 그래프** — 매 이터레이션마다 새로 구성 (파이썬 제어 흐름 지원)
- **Leaf 텐서** — grad_fn 없음 (보통 모델 파라미터), `.grad`에 그래디언트 축적
- **Non-leaf 텐서** — grad_fn 있음, 중간 결과

#### 그래디언트 모드
- **기본 모드** — requires_grad 따라 동작
- **no_grad 모드** — 기록 안 함, 출력은 이후 grad 모드에서 사용 가능
- **inference_mode** — no_grad보다 더 빠름, 대신 이후 autograd에서 사용 불가

#### 주의사항
- **In-place 연산** — 그래디언트 계산에 필요한 값을 덮어쓸 수 있음. 버전 카운터로 감지
- **retain_graph=True** — backward() 후 그래프 유지 (기본은 해제)
- **create_graph=True** — 2차 미분 가능 (Hessian 등)
- **멀티스레드** — 공유 입력에 대한 concurrent backward는 non-deterministic

#### Wirtinger 미적분
- 복소수 텐서 + 실수 손실 → ∂L/∂z* 계산 (켤레 방향)

### 4. torch.optim (일부)

#### 주요 옵티마이저 (WebFetch 제한으로 목록만)
- `SGD` — 기본 경사하강법, 모멘텀/네스테로프 지원
- `Adam` — 적응적 학습률, β1/β2/eps/weight_decay
- `AdamW` — 분리된 가중치 감쇠
- `LBFGS` — Limited-memory BFGS
- `RMSprop`, `Adagrad`, `Adadelta`, `Adamax`, `RAdam`, `NAdam`, `SparseAdam`

#### LR 스케줄러
- `StepLR`, `MultiStepLR`, `ExponentialLR`, `CosineAnnealingLR`, `ReduceLROnPlateau`, `CyclicLR`, `OneCycleLR`, `LinearLR`, `PolynomialLR` 등

### 5. torch.cuda (CUDA 시맨틱)

#### 디바이스 관리
- 기본적으로 현재 선택된 디바이스에 할당
- `torch.cuda.device()` 컨텍스트 매니저로 디바이스 선택
- 크로스 GPU 연산은 `copy_()`, `to()`, `cuda()`로만 가능

#### 비동기 실행
- GPU 연산은 기본 비동기 — 큐에 넣고 나중에 실행
- 디버깅: `CUDA_LAUNCH_BLOCKING=1`로 동기 모드
- 정확한 타이밍: `torch.cuda.synchronize()` 또는 `torch.cuda.Event(enable_timing=True)`

#### CUDA 스트림
- `torch.cuda.Stream()` — 비기본 스트림 생성
- 같은 스트림 내 직렬화, 다른 스트림 간 병렬 실행
- `stream.wait_stream()`, `tensor.record_stream()` — 동기화

#### 메모리 관리
- 캐싱 할당자 — device 동기화 없이 빠른 할당/해제
- `memory_allocated()` vs `memory_reserved()` — 실사용 vs 캐시 포함
- `empty_cache()` — 미사용 캐시 메모리 반환
- `PYTORCH_ALLOC_CONF` — max_split_size_mb, expandable_segments, garbage_collection_threshold 등

#### TensorFloat-32 (TF32)
- Ampere GPU 이상, FP32 입력을 10비트로 라운드 + FP32 누적
- `torch.backends.cuda.matmul.allow_tf32` — A100에서 ~7배 속도

### 6. torch.amp (Automatic Mixed Precision)

#### 핵심 컴포넌트
- **`torch.autocast(device_type, dtype)`** — 자동으로 FP16/BF16 선택
- **`torch.amp.GradScaler()`** — FP16 언더플로우 방지를 위한 그래디언트 스케일링

#### 기본 학습 루프 패턴
```python
scaler = GradScaler()
for input, target in data:
    optimizer.zero_grad()
    with autocast(device_type='cuda', dtype=torch.float16):
        output = model(input)
        loss = loss_fn(output, target)
    scaler.scale(loss).backward()
    scaler.step(optimizer)
    scaler.update()
```

#### 그래디언트 클리핑 시
```python
scaler.scale(loss).backward()
scaler.unscale_(optimizer)  # unscale 먼저!
torch.nn.utils.clip_grad_norm_(model.parameters(), max_norm)
scaler.step(optimizer)
scaler.update()
```

#### 그래디언트 누적
- 스케일된 상태로 누적, step 직전에만 unscale

#### 다중 모델/옵티마이저
- 각 loss 개별 scale, 각 optimizer 개별 step, `update()`는 이터레이션당 1회만

#### 커스텀 autograd Function
- `@torch.amp.custom_fwd()`, `@torch.amp.custom_bwd()` 데코레이터

### 7. torch.save / torch.load (직렬화 상세)

- **state_dict 저장 권장** — 모듈 직접 저장보다 안전하고 호환성 좋음
- **weights_only=True (2.6+ 기본)** — pickle 보안 강화
- **뷰 관계 보존** — 작은 텐서의 뷰가 큰 스토리지 전체를 저장할 수 있음 → `.clone()`
- **FakeTensorMode** — 스토리지 없이 체크포인트 메타데이터만 로드
- **config**: `compute_crc32`, `mmap`, `storage_alignment(64B)`

### 8. torch.compile (컴파일러)

#### 작동 방식
1. **TorchDynamo** (프론트엔드) — 파이썬 코드 심볼릭 추적, 계산 그래프 추출
2. **그래프 최적화** — IR 변환
3. **백엔드 컴파일** — 실행 가능 코드로 변환

#### 주요 함수
- `torch.compile(model, backend=..., mode=...)` — 모델 컴파일
- `list_backends()` — 사용 가능한 백엔드 목록
- `reset()` — 컴파일 캐시 초기화
- `allow_in_graph()` — 심볼릭 추적 건너뛰기
- `disable()` — 컴파일 비활성화 데코레이터

#### 가드 관리
- `skip_guard_on_inbuilt_nn_modules_unsafe()` — 표준 모듈 가드 건너뛰기
- `skip_all_guards_unsafe()` — 모든 가드 건너뛰기

### 9. torch.utils.data (튜토리얼 기반)

#### Dataset
- `__init__()` — 데이터 파일 경로, transform 저장
- `__len__()` — 전체 샘플 수 반환
- `__getitem__(idx)` — 인덱스로 단일 샘플(feature, label) 반환
- `IterableDataset` — 스트리밍/대용량 데이터용

#### DataLoader
```python
DataLoader(dataset, batch_size=64, shuffle=True, num_workers=0, pin_memory=False)
```
- `batch_size` — 배치 크기
- `shuffle=True` — 에포크마다 데이터 셔플 (오버피팅 방지)
- `num_workers` — 멀티프로세스 데이터 로딩
- `pin_memory=True` — CUDA 전송 가속 (GPU 학습 시 권장)
- `collate_fn` — 커스텀 배치 구성 함수
- `drop_last` — 불완전 마지막 배치 버릴지

#### Sampler
- `SequentialSampler`, `RandomSampler`, `SubsetRandomSampler`, `WeightedRandomSampler`, `BatchSampler`, `DistributedSampler`

### 10. 옵티마이저 실전 패턴 (튜토리얼 기반)

#### 기본 학습 루프
```python
optimizer = torch.optim.SGD(model.parameters(), lr=1e-3)
for X, y in dataloader:
    pred = model(X)
    loss = loss_fn(pred, y)
    loss.backward()
    optimizer.step()
    optimizer.zero_grad()
```

#### 옵티마이저 선택 가이드
- **SGD** — 기본, 모멘텀 추가 가능, 대규모 모델에 여전히 유효
- **Adam/AdamW** — 적응적 학습률, 대부분의 딥러닝 작업에 범용
- **RMSprop** — RNN 등 비정상 데이터에 유효
- **lr=1e-3** — 일반적 시작점, 작을수록 느리지만 안정, 클수록 불안정

### 11. Developer Notes — 실전 필수

#### 브로드캐스팅
- 뒤(trailing) 차원부터 비교, 각 차원이 같거나 하나가 1이면 OK
- 결과 크기 = 각 차원의 max
- in-place 연산(`add_` 등)은 원본 shape 변경 불가 → 브로드캐스팅 확장 시 에러
- 예: (5,1,4,1) + (3,1,1) → (5,3,4,1) OK

#### 메모리 포맷 (Channels Last)
- 기본: NCHW contiguous (strides: C*H*W, H*W, W, 1)
- Channels Last: NHWC (strides: C*H*W, 1, W*C, C) — 픽셀 단위 저장
- 변환: `x.to(memory_format=torch.channels_last)` 또는 `.contiguous(memory_format=...)`
- **성능**: GPU에서 22%+ 향상 (FP16+AMP), CPU(Intel)에서 26~76%
- Conv, BatchNorm, pointwise 연산은 포맷 보존. 미지원 연산은 자동으로 contiguous 변환
- 지원 모델: ResNet, VGG, MobileNet, ShuffleNet, DenseNet

#### 재현성 (Reproducibility)
- `torch.manual_seed(seed)` — CPU+CUDA 시딩
- `random.seed()`, `np.random.seed()` — Python/NumPy 별도 시딩
- `torch.backends.cudnn.benchmark = False` — cuDNN 알고리즘 고정
- `torch.backends.cudnn.deterministic = True` — 컨볼루션 결정적
- `torch.use_deterministic_algorithms(True)` — 전체 결정적 모드 (느려짐)
- DataLoader: `worker_init_fn` + `generator` 파라미터로 재현성 확보
- **완전 재현은 보장 불가** (릴리스/플랫폼 간 차이 있을 수 있음)

#### 멀티프로세싱
- `torch.multiprocessing` — 텐서를 공유 메모리로 자동 이동
- CUDA 텐서: `spawn`/`forkserver` 시작 방법 필수 (fork는 CUDA 초기화 문제)
- 보내는 프로세스가 살아있어야 CUDA 텐서 유효
- CPU 과다구독 방지: `set_num_threads(vCPU수 / 프로세스수)`
- `SimpleQueue` > `Queue` (Queue는 백그라운드 스레드 생성)

#### FAQ — OOM 해결
1. **이력 누적 방지**: `total_loss += float(loss)` (loss 자체를 더하면 그래프 유지)
2. **텐서 해제**: `del x` 명시적 삭제
3. **RNN**: truncated BPTT로 시퀀스 분할
4. **Linear 레이어**: 가중치 메모리 = O(n×m), 차원 주의
5. **메모리 체크포인팅**: `torch.utils.checkpoint` — 연산↔메모리 트레이드오프
6. **캐싱 할당자**: nvidia-smi는 캐시 포함 표시, 실제 사용량과 다름
7. **예외 핸들링**: OOM 복구 코드는 except 블록 밖에서 실행

## 미학습 / 추후 학습 예정
- torch.nn.functional 상세 — JS 렌더링으로 추출 실패 (nn 모듈과 1:1 대응이라 급하지 않음)
- 옵티마이저/스케줄러 상세 파라미터 — 필요 시 help()로 직접 확인
- torch.distributed, torch.fx, torch.profiler, torch.sparse — 당장 불필요

## 활용 맥락
- LoRA 학습 (sd-scripts/kohya): nn.Linear, autograd, optim, CUDA, AMP
- RVC 모델 추론: torch.load (weights_only 이슈), CUDA
- LivePortrait: torch.load 패치 (weights_only=True 호환)
- ComfyUI: 전반적인 PyTorch 모델 로딩/추론
- F5-TTS: 모델 추론, CUDA 가속
