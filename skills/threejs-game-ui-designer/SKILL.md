---
name: threejs-game-ui-designer
description: "设计高端的 Three.js 游戏 UI。用于 HUD、菜单、浮层、暂停/胜利/失败界面、设置、图标控件、触控 UI、排版、响应式布局、安全区、文字排布，以及 UI 与场景的协调统一。"
---

# Three.js 游戏 UI 设计师

## 目的

让游戏 UI 有意图、易读、响应式，并契合具体品类。

## 工作流

在设计 HUD、菜单、浮层、暂停/胜利/失败界面、设置、触控、排版、响应式布局、安全区、文字排布、图标或 UI/场景协调时，把加载 `references/ui-patterns.md` 作为第一步。用一张参考台账追踪它，标注是/否、路径和跳过原因。只要这份参考在界面工作中被跳过，就不要把 UI 阶段标记为完成。

在宣称 UI/HUD/菜单工作完成之前，加载 `references/checklists/game-ui-quality.md`、`references/checklists/hud-readability.md` 和 `references/checklists/responsive-ui-fit.md`。当涉及触控或移动端安全区时，加载 `references/checklists/mobile-input.md`。

仅当用户要求可复用提示词、一份 UI 打磨提示词或任务模板时，才加载 `references/prompt-templates.md`。

当 logo、图标、GUI 美术、阵营标记、菜单背景、贴花或 2D HUD 素材能提升质量时，加载 `threejs-image-generator`。`threejs-3d-generator` 仅用于 3D 菜单/展示物体或叙事性 3D UI 道具，不用于普通的扁平 HUD 元素。

1. 抓取/检查桌面和移动端截图。
2. 盘点 UI 状态：玩法中、暂停、设置、失败/重试、胜利/里程碑、加载、触控。
3. 定义层级：生存/状态、目标、反馈、氛围。
4. 用精心设计的组群、量表、徽章、图标、警示和模态状态替换功能性数据卡片。
5. 使用稳定的尺寸、安全区留白、文字排布约束，以及悬停/按下/聚焦/禁用状态。
6. 把 UI 接到游戏状态上，而不是复制一套规则。
7. 核验文字排布、重叠、安全区、触控目标、响应式截图和真实的状态变化。

## 常见失败模式

- 通用的仪表盘/数据卡片式 HUD。
- UI 遮挡了玩家/威胁。
- 文字在移动端发生偏移/裁切。
- 装饰性面板降低了可读性。
- 触控看起来对了，但并未发出意图。

## 最终回复

报告参考台账、UI 状态清单、UI 意图、覆盖的状态、改动的文件、截图、文字排布/重叠检查、安全区/触控目标证据、操作方式，以及尚存的风险。
