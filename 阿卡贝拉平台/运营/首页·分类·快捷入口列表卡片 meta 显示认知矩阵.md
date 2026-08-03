---
title: 首页/分类/快捷入口列表卡片 meta 显示认知矩阵
source: dev_memory/list_meta_cognition_dev_memory.md
project: BERNSINE·阿卡贝拉
tags:
  - 阿卡贝拉
  - 方案策划
---

# 首页/分类/快捷入口列表卡片 meta 显示认知矩阵

## 开发要点
- **宗旨**：列表「显示哪些 meta」服从贴合用户认知——内容流看作者·时间·热度；目录库看身份+热度；乐谱看领域字段；勿全站一套全选
- **权威矩阵**：`_b2child_local/functions-list-meta-cognition.php`
- **内容流**（short/video/quality/tutorial/saishi + 首页推荐）：`user,date,des,like,comment,views`（+video/download/hide）；**不勾 cats**（封面类型角标已表达，分类页再写「短视频」冗余）
- **空摘要（设计规范 §7.7.2 · v2.2）**：网格/瀑布流**一律不占位**（`.b2-excerpt-empty` → `display:none`）。见 `category_post_meta_ui_dev_memory` / `design_system_spec`
- **目录库**（band/musicians/organization/hot_band）：`des,views`（+徽章）；**不勾** user/date/cats/like/comment；**名称 1 行 · 摘要 2 行**（§7.7.6，异于内容流 2/1）
- **内容流字号/边距（2026-07-26）**：与乐团同信息区 pad + 标题 14 / 摘要 12；**行数仍 2/1**，勿混为一谈
- **乐谱**：`views`（+徽章）；改编/演唱由 post-6；不勾 user/date/cats/like/comment/des
- **首页模块**：`new`/`latestarticles`/`video` 同内容流；`wangge`/`pubu` 同目录；`short` 条保留 title/links/des/like/views
- **快捷入口**（自有卡片，非 b2_group）：
  - 快讯：标题+摘要+标签/状态+时间线
  - 专栏：同内容流（作者·时间·热度）
  - 文档：标题+分类芯片
  - 导航：标题+描述（脚注作者/赞已藏）
  - 声场：作者+互动
  - 公告：标题+日期+摘要
  - 练习：声部/调式/BPM/轨数
- **禁止**用 CSS `display:none` 盖 des/user/date（见 `category_post_meta_ui`）；靠取消勾选不输出 DOM
- **日更**：`run.sh list_meta` → `jobs/list_meta_cognition.php`（并顺带 apply 封面比例，见 `list_thumb_ratio_dev_memory`）；cron 上海 **05:48**；状态 `state/list_meta_cognition.json`
- 部署：`_ops_pack/jobs/_deploy_list_meta.py`

## 改动涉及的文件
- `_b2child_local/functions-list-meta-cognition.php`
- `_b2child_local/functions.php`
- `_ops_pack/jobs/list_meta_cognition.php`
- `_ops_pack/run.sh` / `crontab.fragment` / `install_cron.sh`
- 线上分类 `b2_group.post_meta`、`b2_template_index`
- `dev_memory/category_post_meta_ui_dev_memory.md` / `design_system_spec_dev_memory.md` / `ops_scheduler_dev_memory.md`
- `_ops_pack/docs/design_system_spec.md` §7.7

---

> 源文件：`dev_memory/list_meta_cognition_dev_memory.md`（仓库同步；改文请回仓库或再跑同步脚本）

