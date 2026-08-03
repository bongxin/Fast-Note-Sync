---
title: 【设计系统】跨页元素目录 E-*
source: dev_memory/element_catalog_dev_memory.md
project: BERNSINE·阿卡贝拉
tags:
  - 阿卡贝拉
  - 方案策划
---

# 【设计系统】跨页元素目录 E-*

## 工作流（强制）

每次优化**一个页面**时，按序执行：

1. **元素抽取**：列出本页出现的全部 UI 元素（壳层 / 工具条 / 内容 / 操作 / 浮层），打上元素 ID（见下表 `E-*`）。
2. **输出分析**：对照本目录写「分析结果」——已有规范 / 本页偏差 / 应对齐到哪条。
3. **改本页**：只把本页偏差收到规范态；新形态若合理则**回写本目录 + 规范 §7**，禁止只留在单页 CSS。
4. **扩散清单**：在分析结果末列出「同元素出现页」，下页优化时**优先按本表抄，禁止再发明一套**。

### 分析结果模板（每页必出）

```markdown
## 元素抽象 · {页面 ID 名称}

### 本页元素清单
| 元素 ID | 本页选择器/位置 | 目录态 | 本页现状 | 动作 |
|---------|-----------------|--------|----------|------|
| E-chip-filter | … | 规范 | 偏差简述 | 对齐 / 已合 / 例外§9 |

### 偏差结论
- …

### 同元素待对齐页（下页优先）
- Pxx.x …
```

---

## 元素目录（跨页唯一真源）

> 高度/色值以**当前落地为准**；与 `design_system_spec` 冲突时先改规范再改代码。  
> 芯片高：**28**（`--b2-filter-chip-h`）；规范 §7.1 若仍写 24 视为过期。

### E-shell · 壳层

| ID | 名称 | 规范要点 | 典型选择器 | 已见页面 |
|----|------|----------|------------|----------|
| E-shell-list-bg | 主页面背景色 | **`#f5f6f7` 中性冷灰**；`body`/`#page` 实心；**`#content` / 列表壳** 用 `--b2-list-bg-surface`（顶/底向白）；**分类**须在 `#primary-home`/`.post-list` 再刷一层（筛选栏下才可见）；`:is()`；`:root` 同步 style+FOUC+critical | `body.*` / `#page` / `#content` / `.post-list` / FOUC / `functions.php` | 首页、分类、快讯、声场… |
| E-shell-pad-x | 列表左右 gutter | 12；禁双重 pad | `--b2-m-list-pad-x` | 全列表 |
| E-shell-header | 顶栏（快捷入口栏+搜索栏） | 声场可无搜索栏 | `.site-header` / `.b2-m-search-row` / `.header-banner-left` | G01–G03 |
| E-shell-tabbar | 标签栏 | 仅移动；桌面 `display:none`；高 62+safe；选中品牌；**切页瞬时切线框/填充**；**首屏 critical 须 fixed 贴底**（勿等 mobile.css）；沟通勿称「底栏」 | `#mobile-footer-menu` | G04 |
| E-shell-nav-post | 导航栏 | `post` 序；选中酒红+贴底粗指示条；**无底部分界线**；与搜索栏间距用 **padding-top**（勿 margin，防刷新透灰） | `.b2-m-nav` / `.b2-m-nav__item` | G02 |
| E-shell-shortcut | 快捷入口栏 | `ym-menu` 序：快讯→练习→声场→专栏→文档→导航→公告→认证 | `.header-banner-left .menu` | G01 |
| E-shell-search | 搜索栏 | 移动：头像+全站搜；≠ 筛选栏内本类搜 | `.b2-m-search-row` | G03 |
| E-shell-footer | 页脚/标签云 | 功能页可藏 | `.site-footer` / `.widget_tag_cloud` | G07 |
| E-shell-bella | AI 贝拉 | 移动：标签栏中心；关态藏悬浮球。桌面：右下悬浮球 | `#mobile-footer-menu .b2-nav-bella` / `#acappella-qa-widget` | G09 |

### E-filter · 筛选与工具条

| ID | 名称 | 规范要点 | 典型选择器 | 已见页面 |
|----|------|----------|------------|----------|
| E-chip-filter | 标签筛选栏芯片 | 高 **28**、r4、未选 `#f7f7f7`/`#666`、透明边；选中 soft+品牌描边；字 12/400 | `.b2-facet-chip` / `.b2-*-filter__chip` / 声场 `.topic-type-menu button` | 分类、快讯、专栏、文档、导航、声场、收藏 |
| E-filter-bar | 筛选栏 / 工具栏容器 | 白底；上下 pad **4**；芯片 gap **8**；沟通：整块称工具栏，上半行称筛选栏、下半称标签筛选栏 | `.b2-nf-filter` / `.b2-col-filter` / `.tax-info` + `.b2-facet-bar` / `.topic-type-menu` | 同上 |
| E-filter-funnel | 筛选漏斗钮 | 同芯片高；漏斗 SVG 在文字右 | `.fliter-button` / `.topic-drop>button` / `.b2-filter-funnel` | 分类、声场 |
| E-filter-drawer | 移动筛选抽屉 | 右抽屉 + 遮罩；头/完成脚 | `.b2-filter-drawer` / 声场 `.topic-drop-box` | 分类、声场 |
| E-filter-panel | 桌面筛选面板 | 多行维度；选中语义同 facet | `#filter-top` | 分类桌面 |
| E-sort-chip | 排序芯片/下拉 | 视觉跟 facet；勿第三套色 | `.b2-nf-sort` 等 | 快讯等 |

### E-card · 列表内容

| ID | 名称 | 规范要点 | 典型选择器 | 已见页面 |
|----|------|----------|------------|----------|
| E-card-list | 列表项 | r10、卡距 10、白底、无重阴影；沟通勿称「列表卡」 | `.post-info` 卡 / 快捷白卡 | P01–P14、P16、P20 |
| E-card-title | 列表标题 | 14/400；行数按 §7.7.6 | 卡内标题 | 同上 |
| E-card-excerpt | 列表摘要 | 12/muted；空不占位 | 卡内摘要 | 同上 |
| E-card-meta | 作者·时间·热度 | 10–12 / `--b2-meta`；矩阵 §7.7.1 | 卡底 meta | 同上 |
| E-card-cover | 封面+角标+热度叠层 | 同族比；底缘热度 | 封面图 | 内容流 |
| E-card-row | 乐谱行 | L-row；通栏分割非白卡网格 | `.post-6` 等 | P06 |
| E-card-topic | 声场话题卡 | 酷安布局；底栏三等分 | `.circle-topic-item` | P16 |
| E-card-tag-cat | 卡底分类标签 | 迷你 facet：高 20、r4、`--b2-filter-chip` 底 / 灰字 11；纯文字 | `.b2-card-tag--cat` / `.b2-nf-foot .new-tag` | P10 快讯；专栏等可复用 |
| E-card-tag-status | 卡底状态标签 | 高 20、r4、描边；upcoming 蓝 / ongoing 品牌 / ended 灰 | `.b2-card-tag--status` / `.b2-nf-status` | P10 快讯 |
| E-filter-bar-gap | 筛条块间距 | 芯片横滑块与排序/操作块 **gap≥10**；竖向分隔用 **短线**（高≈14、居中），勿通栏 `border-left` | `.b2-nf-sort--dropdown::before` | P10；其它筛条同构时抄 |
| E-shell-tabbar-hide | 标签栏上滑藏净 | `footer-down` 须 `translateY(100%+28px)` + `overflow:hidden`（贝拉头像上探） | `#mobile-footer-menu.footer-down` | 全局 |

### E-read · 阅读

| ID | 名称 | 规范要点 | 典型选择器 | 已见页面 |
|----|------|----------|------------|----------|
| E-read-h1 | 详情标题 | 20/600/1.38 | `.entry-header h1` | 文章/快讯/文档/公告 |
| E-read-body | 详情正文 | 15/1.75 | `.entry-content` | 同上 |
| E-read-h2 | 文内小标题 | 16/600 | 文内 h2–h4 | 同上 |
| E-read-comment-bar | 说点什么底栏 | 移动；贴底+safe | `.b2-m-comment-bar` | 文章/声场详情 |

### E-action · 操作

| ID | 名称 | 规范要点 | 典型选择器 | 已见页面 |
|----|------|----------|------------|----------|
| E-btn-primary-sm | 紧凑主按钮 | 高 **28** / r **14** / pad **0 12** / 字 **12/600**；品牌底 + 白字；已选/已关注 → 浅灰底灰字 | `.b2-m-single-bar__follow` · `.b2-search-ui__submit` | 文章顶栏关注、搜索页「搜索」 |
| E-btn-primary-md | 行内主按钮 | 高 **32** / r **16** / pad **0 12** / 字 **13/500**；品牌底 + 白字 | `.content-ds #TA-con` · 评论提交（可收敛） | 文章打赏、评论发 |
| E-btn-primary-block | 块级/弹层主按钮 | r **999**、通栏或宽；字 14–15/600；品牌底 | `.modal.ds-box .pay-button` · jubao · 登录提交 | 打赏弹层、举报、登录 |
| E-btn-primary-grad | 渐变主按钮（例外） | mid→brand 渐变 + 轻阴影 | `.po-topic-button` · `.b2-write-topbar__pub` | 声场发帖、写作发布 |
| E-btn-secondary | 次按钮 / 已关注 | 浅底或描边；勿实心品牌 | `.empty` · `.is-on` · `.author-has-follow` · `.b2-cu-follow` | 用户搜关注、圈子成员、顶栏已关注 |
| E-btn-text | 文字按钮 | 品牌字无厚底 | `button.text` | 评论取消/点赞等 |
| E-btn-chip | 表单内搜索清空 | 20 圆、浅灰半透明底、细描边 SVG × | `.b2-fs-search__clear` · `.b2-tax-search__clear` · `.b2-search-ui__clear` | 全屏搜、分类搜、搜索页 |
| E-input-search-pill | 搜索输入胶囊 | 高 **34**、r **999**、底 `#f2f3f5`；≠ 主按钮 | `.b2-m-search-btn` · `.b2-search-ui__capsule` | 首页搜栏、搜索页 |
| E-fab | 发帖 FAB | 品牌实心圆；发帖打开时藏 | `.b2-circle-fab` | 声场 |

#### 按钮/表单 · 跨页对照（2026-07-26 梳理）

| 族 | 已合规范 | 待对齐 / 偏差 |
|----|----------|----------------|
| sm 紧凑主 CTA | 文章「关注」、搜索页「搜索」 | 用户搜实心关注、粉丝列表关注（现 r6）、圈子审核钮 |
| md 行内主 CTA | 文章「给TA打赏」≈md | 评论提交 36/r18、声场评论 32/r16 → 应收到 md |
| 弹层通栏 | 打赏/举报/登录 | — |
| 渐变发布 | 声场/写作 | 保留例外，勿当普通 sm |
| 搜索提交 | 搜索页已合 sm | **全屏弹层** `.b2-fs-search … search-button` 仍 **高40/r10** → 应收到 sm 或 md |
| 次态关注 | 顶栏 `.is-on`、用户搜描边 | 作者页顶栏关注仍吃父主题 `.button`，几何与色未完全子主题化 |
| 清空 × | 三处 clear 同款 | — |
| 输入胶囊 | 首页/搜索页同 34 胶囊 | 分类工具条搜、圈子话题搜可抽检 |

### E-overlay · 浮层

| ID | 名称 | 规范要点 | 典型选择器 | 已见页面 |
|----|------|----------|------------|----------|
| E-sheet | 底部 Sheet | 顶角 16；暖米或白；锁滚 | 登录/发布/评论抽屉 | P22/P23/评论 |
| E-modal | 居中弹层 | 桌面居中；移动可降为 Sheet | 海报/举报 | R.4/R.5 |
| E-compose-full | 全屏编辑 | 白底沉浸；藏壳层 | `#show-form` / write v3 | 声场发帖、写作 |

### E-empty · 空态

| ID | 名称 | 规范要点 | 典型选择器 | 已见页面 |
|----|------|----------|------------|----------|
| E-empty | 空状态 | `.b2-empty-state` 统一文案语气 | `.b2-empty-state` | P24 |

---

## 偏差台账（抽取时追加，对齐后删或标 ✅）

| 日期 | 页 | 元素 ID | 偏差 | 状态 |
|------|-----|---------|------|------|
| 2026-07-26 | P16 声场 | E-filter-bar | 条 pad 10/12，他页 4 | ✅ 已改 4 |
| 2026-07-26 | P14 公告 | E-shell-pad | 搜索行下顶距过大 | ✅ 已改 -8+4 |
| 2026-07-26 | P16 发帖 | E-compose-full | 浮卡/彩虹图标/关钮失效 | ✅ 已改 |
| 2026-07-26 | P10.1 快讯 | E-shell-list-bg | 暖米托底不适合 → `#f5f6f7` | ✅ |
| 2026-07-26 | P10.1 快讯 | E-filter-bar-gap | 芯片块贴排序 | ✅ gap10+左边线 |
| 2026-07-26 | 全局 | E-shell-tabbar-hide | 贝拉上探露边 | ✅ +28px overflow |
| 2026-07-26 | P10.1 快讯 | E-card-tag-cat | 分类标签未抽象 | ✅ 迷你 facet |
| 2026-07-26 | 全局 | E-shell-list-bg | FOUC critical 仍写 `#f7f3f1` 盖过 style | ✅ `functions-list-fouc.php` → `#f5f6f7` |
| 2026-07-26 | G 壳 | E-shell-nav-post | 主导航下横线（壳层分界线）不要 | ✅ 去 `.b2-m-nav` border-bottom |
| 2026-07-26 | G 壳 | E-shell-header | 快捷入口页搜索栏下发丝线 | ✅ 去 shadow + minH88 + ::after 盖缝 |
| 2026-07-26 | 快捷入口 | E-filter-bar | 标签筛选栏底边线 | ✅ nf/col/links/doc `border-bottom:0` |
| 2026-07-26 | G 壳 | E-shell-list-bg | FOUC critical 仍写 `#f7f3f1` 盖过 style | ✅ → `#f5f6f7` |
| 2026-07-26 | 搜索页 | E-btn-primary-sm | 「搜索」高34/r999/14/500 ≠ 关注 28/r14/12/600 | ✅ 已合 sm Token |
| 2026-07-26 | 全屏搜弹层 | E-btn-primary-sm | submit 高40/r10 方钮 | 待对齐 |
| 2026-07-26 | 多页 | E-btn-primary-md | 打赏32 / 评论36 / 声场评32 未统一 Token | 待收敛 |

---

## 改动涉及的文件

- 本文件（元素真源 + 偏差台账）
- `page_audit_checklist_dev_memory.md`（页清单）
- `_ops_pack/docs/design_system_spec.md` §7（组件条款；改元素须同步）
- 各页优化时的分析结果（可贴会话，摘要回写本表）

---

> 源文件：`dev_memory/element_catalog_dev_memory.md`（仓库同步；改文请回仓库或再跑同步脚本）

