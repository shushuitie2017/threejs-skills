<div align="center">

# 🎮 Three.js Skills · 中文版

> *「你负责说想要什么游戏，剩下的九个工匠自己动手。」*

![License](https://img.shields.io/badge/License-MIT-9B8CFF)
![Three.js](https://img.shields.io/badge/Three.js-浏览器3D-000000)
![Claude Code](https://img.shields.io/badge/Claude%20Code-·%20Codex-5B8CFF)
![Skills](https://img.shields.io/badge/技能-9%20个专家-32E0FF)

**把 9 个 Three.js 游戏开发专家技能装进你的 AI Agent——你只用一句话说清想要什么游戏，「游戏总监」自动调度玩法、画质、UI、建模、音频、调试、质检，直到跑出一个能玩、能上线的浏览器 3D 成品。**

<sub>不是又一份 Three.js 教程 —— 是一套能让 Claude Code / Codex 真正“做完一个游戏”的技能编排系统。</sub>

[看效果](#-效果示例) · [快速开始](#-快速开始) · [九个技能](#-九个技能它们各管什么) · [可选-api-密钥](#-可选-api-密钥) · [背后的故事](#-背后的故事) · [English](#english)

</div>

---

## 🔥 效果示例

装好技能后，在一个空文件夹里打开 Claude Code / Codex，**只说一句话**，点名总监技能：

```text
用 threejs-game-director 从零做一个精品未来风的塔防游戏。
自动调用玩法、画质、UI、建模、音频、调试、质检各技能。
先做出能玩的循环，再迭代到通过浏览器、移动端、视觉、UI、性能、发布各项检查。
```

Agent 接下来会**自己**做完这些，而不用你逐个点名专家技能：

```text
✓ 加载 threejs-game-director → 拆解为 玩法 / 画质 / UI / 资产 / 音频 / 调试 / 质检 各阶段
✓ 用内置 Vite + TypeScript + Three.js 脚手架起项目
✓ 先跑出一个能玩的核心循环（可控、有目标、有胜负）
✓ npm run build → 浏览器实跑 → 控制台报错检查 → Playwright 截图
✓ 画布非空像素检查 → 桌面/移动端视口 → 主操作交互验证
✓ 填「视觉评分卡」，把原型级和精品级分清楚，剩余风险写明
```

> **它的价值不在“会写 Three.js”，而在把“做一个游戏”这件事拆成有验收、有证据、有台账的流水线——不让原型级的东西冒充精品。**

## 🚀 快速开始

**方式一 · 克隆后本地安装（推荐，最稳）：**

```bash
git clone https://github.com/shushuitie2017/threejs-skills.git
cd threejs-skills
./install.sh --claude      # 装进 Claude Code；Codex 用 --codex；两个都装 --all
```

**方式二 · 一行远程安装（skills CLI）：**

```bash
pnpm dlx skills add shushuitie2017/threejs-skills --skill '*' -a claude-code -g -y
```

安装器只把 `skills/` 复制进对应 agent 的技能目录；同名技能默认跳过（`--force` 覆盖），也**绝不删除**你其它无关技能（除非显式 `--prune-managed`）。

装好后，在你的项目里对 agent 说出你想要的游戏、点名 `threejs-game-director` 即可——它会拉起需要的专家技能。

## 🧩 九个技能：它们各管什么

| 技能 | 管什么 |
|---|---|
| 🎬 **threejs-game-director** | **总入口**：完整游戏搭建与编排，自动分阶段调度其余技能 |
| 🕹️ **threejs-gameplay-systems** | 可玩循环、架构、机制、实体、输入、相机、物理、手感 |
| 🎨 **threejs-aaa-graphics-builder** | 视觉评分卡、资产架构、模型、材质、光照、VFX、渲染打磨 |
| 🖼️ **threejs-game-ui-designer** | HUD、菜单、浮层、响应式布局、图标、安全区、触控 |
| 🐛 **threejs-debug-profiler** | 黑屏、运行时报错、加载/缩放/移动端 Bug、性能与渲染指标 |
| ✅ **threejs-qa-release** | 生产构建、浏览器质检、截图、画布像素、移动端检查、发布风险报告 |
| 🧊 **threejs-3d-generator** | Tripo API 文/图生 3D、纹理、骨骼绑定、动画、GLB/FBX 资产 |
| 🖌️ **threejs-image-generator** | Gemini 生成概念原画、纹理、贴花、天空、图标、界面美术、图生 3D 源图 |
| 🔊 **threejs-audio-generator** | ElevenLabs 音效、环境音、界面音、解说/配音 TTS、变声、降噪 |

**每个技能自带 `SKILL.md`、参考资料、检查清单、脚本，安装后自包含，不依赖仓库根目录的文档。**

## 🔑 可选 API 密钥

核心 Three.js 技能**不需要任何付费密钥**就能用。缺密钥时，总监会报告凭据探测结果、跳过外部生成、回退到程序化/本地资产。只在你想让 agent 生成外部模型/图像/音频时才配：

| 提供方 | 技能 | 环境变量 | 用途 |
|---|---|---|---|
| Tripo | `threejs-3d-generator` | `TRIPO_API_KEY` | 文/图生 3D、可直接用于游戏的 GLB/FBX 主角/载具/道具、纹理、绑定、动画 |
| Gemini | `threejs-image-generator` | `GEMINI_API_KEY` | 概念原画、图生 3D 源图、纹理、贴花、天空、图标、界面美术 |
| ElevenLabs | `threejs-audio-generator` | `ELEVENLABS_API_KEY` | 音效、环境音、界面音、解说/对白 TTS、变声、音频清理 |

> **红线：绝不把 API 密钥提交进 git、也绝不写进浏览器端游戏代码。** 技能只在本地 agent 工具里调用这些 API，再把生成的资产存进你的游戏项目。

## ⚙️ 工作原理

1. **一个总监，八个专家**——`threejs-game-director` 拿到需求后拆阶段、点名对应专家技能，你不必手动选。
2. **证据驱动**——每步产出都要有构建、浏览器实跑、截图、像素检查、视口检查作证，才允许声称“做完”。
3. **自包含脚手架**——从空文件夹起步时，内置 Vite + TypeScript + Three.js 游戏脚手架直接开跑。
4. **精品有门槛**——「视觉评分卡」把原型级和精品级分开，占位方块、静态场景、没验证的截图不算精品。

## 🙏 诚实边界

- **这是开源技能包的中文改编版**：技能定义（9 个 `SKILL.md`）与说明已全面中文化；深层 `references/` 技术参考目前仍是英文，会按需逐步中文化。
- **不自带可玩 demo**：本仓库是让你的 agent 去**造**游戏的技能，不附带成品游戏站点。
- **需要 Claude Code 或 Codex**：它是给这类编码 agent 用的技能编排，不是独立可执行程序。
- **AI 不保证一次到位**：它把流程、验收和回退讲清楚，但复杂游戏仍需你参与迭代与判断。

## 📖 背后的故事

大多数 “AI 做游戏” 的尝试卡在同一处：agent 能拼出一个能跑的场景，却止步于占位方块和静态画面，把原型当成品交付。缺的从来不是“会不会写 Three.js”，而是**一套把“做完一个游戏”拆成阶段、逐项验收、留下证据的方法**。

**Three.js Skills** 把这套方法固化成 9 个协作技能：一个总监统筹，八个专家各守一段产线，从可玩循环到发布质检环环相扣。它在意的不是“能生成”，而是**能不能像手艺人一样把活干完、干到能上线**。

## 👤 关于作者

**蓝猫 · BlueCat** —— AI-native builder，做能上线的中英日三语产品。

| | |
|---|---|
| 🌐 站点矩阵 | [bluecatbot.com](https://bluecatbot.com) |
| 🐙 GitHub | [@shushuitie2017](https://github.com/shushuitie2017) |

<div align="center">
<img src="./assets/contact-qr.jpg" alt="加微信 · 聊 AI 游戏开发" width="200"><br>
<sub>👆 微信扫码，聊 AI × 游戏开发</sub>
</div>

### 也在做

- 🧊 **[蓝猫 3D](https://3d.bluecatbot.com)** —— AI × 3D 角色产线的工具榜单 + 九步实战课
- 🎨 **[矢安 SVGSafe](https://svg.bluecatbot.com)** —— 授权清晰的免费 SVG 图标 / 插画库，6000+ 张
- 🐱 **[蓝猫学 Claude](https://learn.bluecatbot.com)** —— 儿童向 Claude 互动小课本

## 📄 许可证

**MIT —— 随便用，随便改，随便造。**

---

## English

**Three.js Skills (中文版)** is a Chinese adaptation of a self-contained skill package for building playable, polished **Three.js browser games** with Claude Code / Codex. Install the 9 skills, then just tell your agent what game you want and name `threejs-game-director` — it routes gameplay, graphics, UI, asset/audio generation, debugging, and release QA automatically, gathering build/browser/screenshot evidence before claiming done.

```bash
git clone https://github.com/shushuitie2017/threejs-skills.git
cd threejs-skills && ./install.sh --claude   # or --codex / --all
```

Core skills work without paid API keys (procedural/local fallback). Optional keys — `TRIPO_API_KEY`, `GEMINI_API_KEY`, `ELEVENLABS_API_KEY` — unlock 3D / image / audio generation. **Never commit API keys or ship them in browser-side code.** MIT licensed.

---

<div align="center">

*你负责说想要什么游戏，剩下的九个工匠自己动手。*

**[🐙 GitHub · shushuitie2017/threejs-skills](https://github.com/shushuitie2017/threejs-skills)**

</div>
