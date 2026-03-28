---
name: FFmpeg 공식 문서 학습 완료
description: FFmpeg 공식 문서 전체 학습 완료 (6파트) — ffmpeg 기본, ffprobe, Codecs, Formats, Filters, Scaler/Resampler
type: reference
---

FFmpeg 공식 문서 (https://www.ffmpeg.org/documentation.html) 전체 학습 완료 (2026-03-28).

## 학습 범위 (6파트)

1. **ffmpeg 기본** — 파이프라인(Demux→Decode→Filter→Encode→Mux), 옵션 체계, -map 스트림 선택, 필터그래프 문법, 2-pass 인코딩, HW 가속
2. **ffprobe** — 미디어 분석, -show_format/-show_streams, JSON/XML/CSV 출력, -select_streams, -read_intervals 구간 지정
3. **Codecs** — H.264(libx264)/H.265(libx265)/AV1(libaom-av1)/VP9(libvpx-vp9) 비디오 코덱, AAC/Opus/MP3(LAME)/FLAC/Vorbis 오디오 코덱, CRF/프리셋/프로필/튜닝/레이트컨트롤
4. **Formats** — MP4/MKV/WebM/AVI/TS/FLV 컨테이너, movflags(faststart/dash/frag_keyframe), concat 디먹서, image2(이미지 시퀀스), DASH/HLS 먹서, segment 먹서
5. **Filters** — 비디오 293개 + 오디오 122개 + 멀티미디어 필터. 핵심: scale/crop/overlay/drawtext/pad/fade/xfade/zoompan/hstack/vstack/eq/colorbalance/curves + loudnorm/afade/atempo/amix/acompressor/equalizer + concat/select/setpts/split
6. **Scaler/Resampler** — 스케일링 알고리즘(lanczos/bicubic/bilinear/point), 디더링, 리샘플링 엔진(swr/soxr), 채널 믹싱, 매트릭스 인코딩

## 활용 맥락
- MOKA's Diary 영상 파이프라인 (ComfyUI 출력 → 영상 편집)
- 게임 트레일러/PV 제작
- OSMU 콘텐츠 파이프라인 영상 처리
