---
name: threejs-gameplay-systems
description: "构建并迭代可玩的 Three.js 游戏系统。整合了起步脚手架创建、架构、玩法实现以及手感调校。用于首个可玩切片、新的 Vite/TypeScript/Three.js 游戏搭建、游戏循环、实体系统、input、collision/physics、scoring、objectives、音频钩子、camera、controls、难度、反馈以及可维护的结构。"
---

# Three.js 玩法系统

## 目的

创建或演进一个可玩的浏览器游戏循环，具备清晰的归属划分、灵敏的操作、确定性的更新顺序，以及经过验证的面向玩家的行为。

## 何时使用

开始一款新游戏、修复孱弱的原型、添加机制/实体、设计架构、调校相机/操作、实现规则/目标，或改善手感时。

## 工作流

当任务包含首个可玩搭建、架构、机制、实体、输入、相机、碰撞/物理、计分、目标、反馈或手感调校时，第一步就加载 `references/gameplay-workflows.md`。

在新增或修改物理、重碰撞玩法、载具移动、滚动球、迷你高尔夫、台球/斯诺克、弹球、刚体解谜、角色控制器、传感器、高速抛射物、移动平台或物理 QA 之前，先加载 `references/physics-engine-selection.md`。用一份引用台账追踪这两份引用，记录 是/否、路径和失败原因。若某份所需引用被跳过，不要把玩法阶段标记为完成。

在宣称一款新游戏或首个可玩切片完成之前，先加载 `references/checklists/new-game-definition-of-done.md`。

无尽跑酷类工作先加载 `references/checklists/endless-runner-premium-quality.md`。

仅当用户请求可复用的提示词、起步提示词或任务模板时，才加载 `references/prompt-templates.md`。

当实现真实音效、环境声、UI 音效、人声/TTS 或超出简单占位钩子的音频清理时，加载 `threejs-audio-generator`。玩法代码应发出音频事件；音频技能应生成或处理实际资产并定义运行时音频矩阵。

1. 检查项目结构、脚本、依赖、当前循环、输入、相机、实体、状态、UI 和诊断。
2. 定义一句话可玩循环：动词、目标、反馈、失败/重试。
3. 选择小而清晰的架构边界：`core`、`game`、`entities`、`systems`、`assets`、`ui`、`tests`。
4. 以可玩的增量实现机制：输入、状态、实体、碰撞/物理、反馈、HUD/音频钩子、诊断。
5. 调校手感：移动、加速、相机跟随/FOV/抖动、冲击、冷却、难度、重启循环。
6. 让热路径保持低分配，并显式规定更新顺序。
7. 通过构建、浏览器、截图、canvas 像素、控制台/页面错误以及一条真实输入路径进行验证。

## 打包脚手架

在开始新项目或用户要求起步游戏时，使用捆绑的脚手架：

```bash
python3 <this-skill-dir>/scripts/create_threejs_game.py ./my-game
```

该脚本会复制 `assets/threejs-vite-game/`，在 `package.json` 和 `package-lock.json` 中改写项目名，并让生成的游戏自包含，各自带有独立的视觉测试和 canvas 检查脚本。仅当目标目录可以被覆盖时才使用 `--force`。

## 库使用指引

- 使用 TypeScript、Vite、Three.js 模块。
- 简单的街机式触发器和拾取物用自定义碰撞。
- 对于带刚体、传感器、球体、斜坡、大量接触点或高速碰撞的正式 Three.js 浏览器游戏，Rapier 是默认的稳健物理引擎。
- 仅把 `cannon-es` 当作小型/简单刚体场景的轻量级 JS 回退方案。
- 当作者主导的街机手感比模拟更重要时，使用自定义碰撞。
- 有需要时用 `lil-gui` 实时调校常量。
- 运行时播放和程序化反馈用 Web Audio；生成的游戏音频资产用 `threejs-audio-generator`。

## 常见失败模式

- 做成静态演示而非可玩循环。
- 机制能编译但无法被真实输入触发。
- 相机/操作感觉延迟，或遮住了下一步决策。
- 状态变化没有驱动 UI/音频/VFX。
- 抽象在机制需要之前就提前出现。

## 最终回复

报告引用台账、玩法清单结果、行为、操作、改动的文件、架构选择、调校后的数值、验证证据、产物以及尚存的边缘情况。
