---
author: unknown
source: theme-plume.vuejs.press
url: https://theme-plume.vuejs.press/guide/embed/video/bilibili/#%E8%AF%AD%E6%B3%95
saved: 2026-06-30 18:39:28
tags:
  - 笔记同步助手
id: a9a8d9a5-2b13-4ecf-89a0-994404a17804
---

1.  [首页](/)
2.  指南
3.  资源嵌入
4.  [Bilibili 视频](/guide/embed/video/bilibili/)

复制页面

## [概述](#概述)

主题提供了 嵌入 Bilibili 视频 的功能。

该功能由 [vuepress-plugin-md-power（在新窗口打开）](../../config/plugins/markdownPower.md) 提供支持。

## [配置](#配置)

该功能默认不启用。你需要在主题配置中开启。

.vuepress/config.ts

```
export default defineUserConfig({
  theme: plumeTheme({
    markdown: {
      bilibili: true, 
    },
  })
})
```

## [语法](#语法)

简单的语法：

```
@[bilibili](bvid)
```

带 分P 的视频，在 `bilibili` 后跟随 `p1`、`p2`、`p3` 等选项

```
@[bilibili p1](aid cid)
```

更多选项：

```
@[bilibili p1 autoplay time="0" width="100%" height="400px" ratio="16:9"](bvid aid cid)
```

**选项说明：**

-   bvid: 视频 BV ID
-   aid: 视频 AID
-   cid: 视频 CID
-   autoplay: 是否自动播放
-   time: 视频开始播放时间点，单位为秒， 也可以使用 `mm:ss` 或 `hh:mm:ss` 格式
-   width: 视频宽度
-   height: 视频高度
-   ratio: 视频比例，默认 `16:9`

对于分P的视频，可以省略传入 `bvid`，但需要传入 `aid` 和 `cid`

## [示例](#示例)

### [宽频视频](#宽频视频)

输入：

```
@[bilibili](BV1EZ42187Hg)
```

输出：

### [竖屏视频](#竖屏视频)

输入：

```
@[bilibili width="320px" ratio="9:16"](BV1zr42187eg)
```

输出：

## [贡献者](#doc-contributors)

## [更新日志](#doc-changelog)

2025/10/7 15:13

查看所有更新日志

-   [`4d236`](https://github.com/pengzhanbo/vuepress-theme-plume/commit/4d2361a7046214fe0f4e4af01831107fd00e38ad)\-feat(theme)!: add collections support ([#704](https://github.com/pengzhanbo/vuepress-theme-plume/issues/704))于 2025/10/7
-   [`0fd6c`](https://github.com/pengzhanbo/vuepress-theme-plume/commit/0fd6cac57412002f4d72dc10378789b529adc357)\-refactor(theme): improve types and flat config ([#524](https://github.com/pengzhanbo/vuepress-theme-plume/issues/524))于 2025/3/15
-   [`bd4c3`](https://github.com/pengzhanbo/vuepress-theme-plume/commit/bd4c3506dc23d42e8e5b5cbf2a7fc9128d2e43fe)\-feat(plugin-md-power): add `artplayer` support ([#393](https://github.com/pengzhanbo/vuepress-theme-plume/issues/393))于 2024/12/21
-   [`9a441`](https://github.com/pengzhanbo/vuepress-theme-plume/commit/9a441c094166d8a5e6a2906dbf45134e7c8f5bb0)\-docs: update doc于 2024/3/29

---

内容效果不满意？[点此反馈](https://feedback.notebooksyncer.com/feedback/9b6d5d04_1782815967237?u=https%3A%2F%2Ftheme-plume.vuejs.press%2Fguide%2Fembed%2Fvideo%2Fbilibili%2F%23%25E8%25AF%25AD%25E6%25B3%2595&s=obsidian)