# Changelog

本仓库采用 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.1.0/) 格式。
版本号在首个正式发布前以里程碑标注；本仓库只承载官网静态站点，无独立版本号，跟随 `index.html` 的实质性改动记录。

## [Unreleased]

含 PR #3（feat: add Ordane marketing site）。

### Added

- 首个可发布的官网页面：hero、line 原语说明、能力清单、三条原则（含可切换 tab）、Runtime 抽象层轨道图、三级收编阶梯、CTA、页脚。内容取自 `org-workbench` 现有仓库事实，附一张该客户端 `examples/oss-maintainer` 示例工作区的真实截图（未经修饰）。
- 导航与 favicon 图标：替换初始占位图形为正式设计稿（teal 环 + 播放三角标记）。

### Fixed

- `mem 长期 Context` 能力状态由 `Shipped` 改为 `Building`，个人版文案由"本地记忆"改为"本地历史 readback"——`org-workbench` README 明确长期 Context 与委派链仍未完成，此前的措辞把未交付能力当成了已发布能力。
- `openai-compatible` Runtime 节点改为虚线、降低视觉权重，标注"Preview · 未 live-qualified"——该能力仅存在于 `digital-employee` 仓库且标注为 preview/fixture-conformant，`org-workbench` 自身未提供对应证据。
- 深色模式 `--ink-3`（56% → 60.7% L）与浅色模式 `--ink-3`（55% → 53.3% L）：对全部三个背景（paper/band/card）的小字号文本对比度均低于 WCAG 4.5:1 门槛（3.81–4.26:1 / 4.31:1），逐一计算 OKLCH → 线性 sRGB → 相对亮度后调整，修复后各组合 4.62–5.20:1。
- 浅色模式 `--amber`（64% → 54.5% L）：`.st-building` 状态标签在浅色模式下对 paper/band/card 均低于 4.5:1（3.13–3.51:1），同一方法计算后调整，修复后 4.60–5.17:1；深色模式 `--amber` 原值已通过，未改动。
