---
title: 视频 AI 解析（评论区问贝拉）方案
source: dev_memory/video_ai_comment_proposal.md
project: BERNSINE·阿卡贝拉
tags:
  - 阿卡贝拉
  - 方案策划
---

# 视频 AI 解析（评论区问贝拉）方案

## 开发要点
- **历史**：阶段一曾跳过；**2026-07-24 P0 已上线**（插件 `acappella-qa` **0.4.7**）。
- **P0 做了什么**
  - 短视频沉浸页左下「问贝拉」；视频/短视频**详情**底栏头像「问贝拉」+ 评论区顶芯片
  - `AcappellaQAUI.openWithContext({ postId, title })`；聊天 REST 增 `post_id`，注入标题/摘要/分类/标签/正文节选 + 优先 RAG 本帖块
  - 本片预设：谁唱的 / 声部 / 一句话 / 练什么；明示**不能看外链画面**
- **未做（P1/P2）**：本片导读缓存；ASR / 关键帧；真多模态
- **入口**：勿替代底栏中心全局贝拉；本片模式仅视频相关页

## 改动涉及的文件
- `_server_plugins/acappella-qa/`：`acappella-qa.php`、`class-chat.php`、`class-rag.php`、`class-frontend.php`、`assets/frontend.js`、`assets/frontend.css`
- `_b2child_local/child.js`、`style.css`
- `b2child-shorts/shorts.php`、`assets/shorts.js`、`assets/shorts.css`
- `dev_memory/acappella_qa_plugin_dev_memory.md`

---

> 源文件：`dev_memory/video_ai_comment_proposal.md`（仓库同步；改文请回仓库或再跑同步脚本）

