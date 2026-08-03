---
title: PDF 乐谱转试听音频（OMR）方案
source: dev_memory/score_pdf_to_audio_proposal.md
project: BERNSINE·阿卡贝拉
tags:
  - 阿卡贝拉
  - 方案策划
---

# PDF 乐谱转试听音频（OMR）方案

## 开发要点
- **结论**：技术上可行，但质量强依赖 PDF 类型；不适合承诺「任意扫描谱 → 真人合唱」。
- **推荐管线**：PDF → OMR → MusicXML/MIDI → 合成/分轨音频 → 站内播放（可挂到 `/practice`）。
- **现状对齐**：站内乐谱多为 PDF Embedder；`score_format` 已含 PDF/MIDI/分轨/音频；练习频道 P0 已有多轨播放；服务器无 GPU → 重模型 OMR/拆轨宜外置或异步队列。
- **PDF 类型差异**
  - 矢量/打印清晰、标准五线谱：OMR 成功率高
  - 扫描件、手写、密集改编谱、特殊记号：易错音/漏声部，需人工校
- **阿卡贝拉注意**：多声部（SATB 等）要按轨输出；合成阶段可用钢琴/合唱音色，真人感需另备分轨素材
- **分期建议**
  - **P0（验证）✅ 2026-07-24**：8 份矢量 PDF → Audiveris → `.mxl` → FluidSynth Choir Aahs；**已上架「可练习」**（分轨练习曲 `omr-score-{id}`，见 `score_practice_link_dev_memory.md` / `_score_omr_publish_practice.py`）
  - 曲目：Deck the Hall、至少还有你、知足、当、心墙、Happy Birthday、Without U、九儿
  - 注意：合成试听有 OMR 误差，非真人分轨
  - **P1（半自动）**：后台「从 PDF 生成试听」任务；成功则写 MIDI/预览 mp3 + 挂练习轨；失败进人工队列
  - **P2（产品化）**：乐谱详情「试听/跟谱」；声部开关；与 practice 关联；可选会员解锁
- **P0 跑通要点**
  - 本机 GitHub 受限；Audiveris `.deb` 用 `ghfast.top` 镜像装到服务器；Windows 包可走 `audiveris.com` CDN（慢）
  - 服务器 3.8G 内存需加 2G swap；batch 用 `xvfb-run`
  - **音色（2026-07-24）**：弃用 soft-organ 正弦垫；改 **FluidSynth + MuseScore_General.sf3**（GM Choir Aahs / prog 52），接近 MuseScore 桌面试听。脚本 `_score_omr_p0_synth_musescore.py` / `_score_omr_p0_render_musescore_resume.py`；SF3 缓存在服务器 `/root/acappella-ops/score_omr_p0/tools/`
  - 粗分桶 8/8 `usable-candidate`（多声部+足够音符）≠ 音高准确率；`Without_U` 小节数偏多、时长偏短，需人工听
  - 优先试听：`Happy_Birthday_A_Capella.wav`、`1-_Deck_the_Hall_SAT.wav`（已换 MuseScore 音色）
- **版权**：仅处理站内有权分发的谱；生成音频同样受原作/改编权约束
- **不建议**：前端纯浏览器实时 OMR 全量；把扫描烂谱当默认输入

## 改动涉及的文件
- `_ops_pack/score_omr_p0/`（samples / omr_out / midi_out / audio_out / P0_REPORT.md）
- `_ops_pack/jobs/_score_omr_p0_prepare.py`
- `_ops_pack/jobs/_score_omr_p0_synth.py`（旧 soft-organ，保留兜底）
- `_ops_pack/jobs/_score_omr_p0_synth_musescore.py`
- `_ops_pack/jobs/_score_omr_p0_render_musescore.py`
- `_ops_pack/jobs/_score_omr_p0_render_musescore_resume.py`
- `_ops_pack/jobs/_score_omr_p0_run.py`
- `_ops_pack/jobs/_score_omr_p0_server_run.py`
- `_ops_pack/jobs/_score_omr_p0_eval.py`
- `dev_memory/multitrack_practice_proposal.md`（P2 MIDI 跟谱可并入本管线）
- `dev_memory/practice_dev_memory.md`
- `dev_memory/score_publish_dev_memory.md`
- 服务器：`/opt/audiveris`、`/root/acappella-ops/score_omr_p0/`、`/swapfile_omr`、fluidsynth + MuseScore_General.sf3

---

> 源文件：`dev_memory/score_pdf_to_audio_proposal.md`（仓库同步；改文请回仓库或再跑同步脚本）

