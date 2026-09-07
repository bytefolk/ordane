# Changelog

本仓库采用 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.1.0/) 格式。
版本号在首个正式发布前以里程碑标注；本仓库只承载官网静态站点，无独立版本号，跟随 `index.html` 的实质性改动记录。

## [Unreleased]

含 PR #3（feat: add Ordane marketing site）。

### Added

- 首个可发布的官网页面：hero、line 原语说明、能力清单、三条原则（含可切换 tab）、Runtime 抽象层轨道图、三级收编阶梯、CTA、页脚。内容取自 `org-workbench` 现有仓库事实，附一张该客户端 `examples/oss-maintainer` 示例工作区的真实截图（未经修饰）。
- 导航与 favicon 图标：替换初始占位图形为正式设计稿（teal 环 + 播放三角标记）。
- `scripts/render-check.js`：站点的渲染校验脚本。无头渲染 `index.html`，对 hero / runtime / ladder 三段分别定位、滚动、截图并检查尺寸与文件大小，逐屏推进滚动以确保 9 个 `.reveal` 区块全部被 IntersectionObserver 触发，点击三条原则的 tab 验证面板切换。**失败即非零退出**（`try/finally` 保证浏览器关闭），判定口径为：
  - **致命**：`pageerror`；页面自身代码产生的 `console.error`；除字体主机以外任何失败的请求；以上各项断言不通过。
  - **非致命但记录**：`fonts.googleapis.com` / `fonts.gstatic.com` 的字体请求失败，按 URL 判定后计入 `WEBFONT_LOAD_FAILURES`——这取决于运行者的网络而非页面本身（未做此分类前，一次运行曾因 4 条 `ERR_NETWORK_CHANGED` 误报失败）。`Failed to load resource` 这类 console 回声不重复计数，统一由 `requestfailed` 分类。

  带 `--self-test-failclose` 会在同一页面注入一条 console 错误和一个抛出的异常，用于证明失败路径确实以非零退出，而不只是打印。

### Fixed

- 手机宽度横向溢出：Runtime 轨道图的三个 Host 节点用 `left: 90%` 等绝对定位 + `white-space: nowrap`，390px 下容器仅约 334px 宽，把文档撑到比视口宽 71px（`docScrollW=461` vs `winW=390`），导致整页可以左右拖动。720px 以下改为纵向堆叠（隐藏轨道圆环、节点转为静态流式布局并允许换行），修复后 390 / 768 / 1440 三个宽度均无横向溢出。
- 浅色模式主 CTA 按钮 hover 对比度：`.btn-primary:hover` 会把背景换成一个更亮的 teal，近白色标签文字掉到 3.90:1（低于小文本 4.5:1 门槛）。语义修正为「浅色底 hover 变深、深色底 hover 变亮」，token 由 `--teal-bright` 更名为 `--teal-hover`（浅色 58% → 40% L），修复后浅色 8.20:1、深色 9.78:1。全站 22 对文字/背景组合 × 明暗两套共 44 项已逐一计算，现全部通过。
- 三条原则的 tab 只实现了半套 ARIA：声明了 `role="tablist"` / `role="tab"` / `aria-selected`，但面板缺 `role="tabpanel"`、按钮缺 `aria-controls`、面板缺 `aria-labelledby`，且没有方向键导航与 `tabindex` 管理——读屏会播报「tab, 1 of 3」而方向键无反应。现补全为完整模式（含 roving tabindex 与 ←/→/↑/↓/Home/End）。
- 标题层级跳级：页脚三个栏目标题为 `<h4>`，其前最近的标题是 CTA 区的 `<h2>`，跳过了 h3。改为 `<h3>`。
- `mem 长期 Context` 能力状态由 `Shipped` 改为 `Building`，个人版文案由"本地记忆"改为"本地历史 readback"——`org-workbench` README 明确长期 Context 与委派链仍未完成，此前的措辞把未交付能力当成了已发布能力。
- `openai-compatible` Runtime 节点改为虚线、降低视觉权重，标注"Preview · 未 live-qualified"——该能力仅存在于 `digital-employee` 仓库且标注为 preview/fixture-conformant，`org-workbench` 自身未提供对应证据。
- 深色模式 `--ink-3`（56% → 60.7% L）与浅色模式 `--ink-3`（55% → 53.3% L）：对全部三个背景（paper/band/card）的小字号文本对比度均低于 WCAG 4.5:1 门槛（3.81–4.26:1 / 4.31:1），逐一计算 OKLCH → 线性 sRGB → 相对亮度后调整，修复后各组合 4.62–5.20:1。
- 浅色模式 `--amber`（64% → 54.5% L）：`.st-building` 状态标签在浅色模式下对 paper/band/card 均低于 4.5:1（3.13–3.51:1），同一方法计算后调整，修复后 4.60–5.17:1；深色模式 `--amber` 原值已通过，未改动。
