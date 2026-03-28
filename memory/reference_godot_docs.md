---
name: Godot Engine Documentation Reference
description: Godot 4.6 공식 문서 전체 학습 완료 (2026-03-28). About/GettingStarted/Manual 21영역/EngineDetails 포함 250+페이지
type: reference
---

Godot 4.6.1 공식 문서 전체 학습 (2026-03-28). docs.godotengine.org → GitHub 원본(godotengine/godot-docs)으로 학습.

# 학습 범위

## About (4p)
- MIT 라이선스, 2001년 아르헨 스튜디오→2014 오픈소스
- 렌더러 3종: Forward+(Vulkan/D3D12/Metal), Mobile, Compatibility(OpenGL)
- 언어: GDScript(권장), C#(.NET8), C++(GDExtension)
- ECS 안 씀 (상속 기반, 자식 노드로 컴포지션)

## Getting Started (29p)
- Introduction 6p: 4대 핵심(Node, Scene, SceneTree, Signal), 에디터 5화면, 설계 철학
- Step by Step 6p: 노드/씬, 인스턴싱, 스크립팅, 입력, 시그널
- First 2D Game 7p: "Dodge the Creeps" — Area2D, 스폰 시스템, HUD, 오디오
- First 3D Game 10p: "Squash the Creeps" — CharacterBody3D, 물리 레이어, 점프/밟기, AnimationPlayer

## Manual (200+p)

### Best Practices (12p)
- 씬 = 의존성 없이 독립 설계, 느슨한 결합 (시그널/Callable/NodePath)
- 의존성 주입 5가지, 형제 통신은 부모가 중재
- Autoload: 넓은 범위 시스템에만 (static func + class_name으로 대체 가능)
- 노드 대안: Object(수동) < RefCounted(자동) < Resource(직렬화)
- 참조 속도: @export > @onready/$Child > get_node()
- 초기화 순서: 초기값 → _init() → Export값 → _enter_tree(하향) → _ready(상향)
- 파일명 snake_case, 노드명 PascalCase, .godot/ 제외, Git LFS 대용량 에셋

### Scripting (26p)
- GDScript: 점진적 타이핑, match 패턴매칭, @abstract(4.5+), 가변인자(...args)
- Export: @export_range/file/dir/flags/enum/group/subgroup/category/storage
- 코드 순서: @tool→class_name→extends→signals→enums→const→static→@export→var→@onready→_init→_ready→_process
- 코어: _process vs _physics_process, 그룹, 씬 고유 노드(%Name), SceneTree, 일시정지(Process Mode), 오토로드, Resource(데이터 클래스), 파일시스템(res:// user://), 로깅, Expression, 크로스 언어(상속 불가)
- 디버깅: 브레이크포인트, Evaluator, Profiler(Self모드), ObjectDB(4.6+), 커스텀 모니터

### 2D (13p)
- 좌표: X→오른쪽+, Y→아래+
- 라이팅: CanvasModulate, PointLight2D, DirectionalLight2D, LightOccluder2D, 노멀맵
- 패럴랙스: Parallax2D, Scroll Scale, Repeat Size
- 타일맵: TileSet(리소스)+TileMapLayer(노드), Terrain 자동매칭, 내비게이션→NavigationRegion2D 베이킹 권장

### 3D (18p)
- 좌표: 오른손법칙, 미터 단위, Y=위, Z=앞
- StandardMaterial3D: PBR(Albedo/Metallic/Roughness/Emission/Normal/AO/SSS/Clearcoat/Anisotropy/Refraction), ORMMaterial3D(채널1장)
- 라이팅: Directional/Omni/Spot, Shadow Bias/Normal Bias
- 최적화: MultiMesh, LOD, Visibility Range, Occlusion Culling, VRS

### Physics (14p)
- 4종: Area(감지), StaticBody(환경), RigidBody(시뮬레이션), CharacterBody(코드 제어)
- Layer(내 위치) vs Mask(탐지 대상), 32레이어
- CharacterBody: move_and_collide(수동) vs move_and_slide(자동 슬라이딩)
- 레이캐스팅: _physics_process 안에서만, PhysicsRayQueryParameters, exclude=[self]

### Animation (7p)
- AnimationPlayer: 키프레임, RESET 애니메이션, Markers
- AnimationTree: BlendTree, StateMachine(travel), Root Motion

### Assets Pipeline (8p)
- 자동 임포트, .import 파일 VCS 포함, ResourceLoader 접근

### Audio (6p)
- dB 스케일, AudioStreamPlayer/2D/3D, AudioStreamRandomizer

### Export (9+p)
- Export Preset, Feature Tags, 커맨드라인 --export-release

### File I/O (5p)
- res://(읽기전용) vs user://(쓰기), 게임 저장 패턴(Persist 그룹+JSON)

### i18n (5p)
- tr()/tr_n(), Named placeholders, 번역 컨텍스트, BiDi/RTL 자동

### Input (7p)
- 흐름: _input→_gui_input→_shortcut_input→_unhandled_key_input→_unhandled_input
- 이벤트(일회) vs 폴링(지속), InputMap

### Math (6p)
- 벡터: normalized/dot/cross/bounce/direction_to
- Transform: 합성(parent*child), 역변환(affine_inverse), 3D회전=Quaternion

### Navigation (14p)
- NavigationRegion/Agent/Obstacle/Link, await physics_frame 후 쿼리

### Networking (6p)
- ENet 멀티플레이어, @rpc("any_peer","call_local","reliable"), HTTPRequest

### Performance (9p)
- Server API(RenderingServer/PhysicsServer) 저수준 최적화

### Plugins (2p)
- @tool + Engine.is_editor_hint(), EditorScript(Ctrl+Shift+X)

### Rendering (6p)
- Viewport, SubViewport, 다중해상도(Stretch Mode/Aspect)

### Shaders (12p)
- 타입: spatial/canvas_item/particles/sky/fog
- 함수: vertex/fragment/light/start/process/sky/fog

### UI (10p)
- Anchors(0~1 비율), Container(HBox/VBox/Grid/Margin/Tab/Split/Scroll)

### XR (15p)
- OpenXR, Quest/Pico/Magic Leap, 핸드/바디 트래킹

### Editor/Migrating/Troubleshooting (17p)
- 프로젝트 매니저, 커맨드라인, 외부 에디터, 4.0~4.6 마이그레이션

## Engine Details (20p)
- 아키텍처: Scene→Server→Drivers 3계층 + Core/Main
- Variant: 24바이트, 37타입, Nil/Object만 nullable
- Object: GDCLASS 매크로, ClassDB 등록, RefCounted=Ref<>
- 렌더링: RenderingDevice 추상화, 클러스터드 라이팅, SDFGI/VoxelGI/LightmapGI, froxel 볼류메트릭 포그
- TSCN: 텍스트 씬 포맷, UID 추적, NodePath 상대경로
