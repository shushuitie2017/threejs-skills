---
name: threejs-game-director
description: "完整 Three.js 浏览器游戏的创建、精品迭代与自动分阶段编排的首要入口。默认用于 build-a-game、升级、打磨、premium、AAA、high-fidelity、from-scratch、endless runner、街机、动作、release-ready 或 showcase 类请求。对于范围较广的工作，先加载用于 gameplay systems、AAA 画质、UI、调试/性能分析、QA/release 的同级公共技能文件。对于带角色、载具、飞船、武器、建筑、标志性道具、天空、纹理、贴花、Logo、图标、GUI 美术、音频/SFX/配音需求或非基础画质的精品游戏，在判定不需要生成资产之前，先加载 threejs-3d-generator、threejs-image-generator 和/或 threejs-audio-generator。维护技能加载、参考文件、资产来源和阶段执行台账，让用户无需手动选择技能。"
---

# Three.js 游戏总监

## 目的

对端到端的游戏成果负全责。搭建可玩循环，路由到正确的阶段，核验证据，绝不把原型级质量的成果称作精品。

## Claude 兼容规则

Claude 风格的技能运行器在用户执行 `/threejs-game-director` 时可能只调用本技能。除非运行器确实调用了其他技能，否则不要声称调用了它们。对于范围较广的工作，你仍必须在规划或编辑前尝试用文件系统读取工具加载同级公共 `SKILL.md` 文件，然后在每个阶段开始前加载该阶段所需的参考文件。如果某个同级 `SKILL.md` 无法加载，就用 `references/director-phase-os.md` 作为该阶段的回退方案，并记录加载失败。

## 强制的同级技能加载

对于完整、premium、AAA、精修、high-fidelity、showcase、from-scratch、升级或 release-ready 的游戏工作，在实现之前加载这些同级技能文件：

- `threejs-gameplay-systems/SKILL.md`
- `threejs-aaa-graphics-builder/SKILL.md`
- `threejs-game-ui-designer/SKILL.md`
- `threejs-debug-profiler/SKILL.md`
- `threejs-qa-release/SKILL.md`

对于 premium、AAA、high-fidelity、showcase、完整、release-ready 或「非基础」的游戏工作，当游戏包含或应当包含高价值 3D 资产时加载此技能：生成的 3D 模型、骨骼绑定、动画、带纹理的导入资产、角色、生物、Boss、建筑、载具、飞船、武器、标志性道具、复杂拾取物或英雄级环境部件。在判定程序化 Three.js 是否足够之前完成此步：

- `threejs-3d-generator/SKILL.md`

对于 premium、AAA、high-fidelity、showcase、完整、release-ready 或「非基础」的游戏工作，当游戏包含或应当包含概念/参考图、纹理参考、材质参考、天空/背景、Logo、标记、图标、贴花、GUI 美术、标题/菜单美术、地形/天空贴片，或作为图生 3D 输入的 2D 图像时加载此技能。在判定不需要这些资产之前完成此步：

- `threejs-image-generator/SKILL.md`

对于 premium、AAA、high-fidelity、showcase、完整、release-ready 或「非基础」的游戏工作，当游戏包含或应当包含 SFX、环境音、UI 音效、交互音频、载具/武器/Boss 音效、播报员/对白、草稿演出的音色转换或音频清理时加载此技能。在判定不需要生成音频之前完成此步：

- `threejs-audio-generator/SKILL.md`

按以下顺序尝试路径：

1. 同级安装路径：`../<skill-name>/SKILL.md`
2. Claude 默认路径：`~/.claude/skills/<skill-name>/SKILL.md`
3. Codex 默认路径：`~/.codex/skills/<skill-name>/SKILL.md`
4. 通用 agents 路径：`~/.agents/skills/<skill-name>/SKILL.md`
5. 仓库源码路径：`skills/<skill-name>/SKILL.md`

如果文件读取工具要求绝对路径，读取前先把 `~` 展开为用户主目录。

对于总监调用的窄范围工作，加载直接相关的同级技能和 `threejs-qa-release`。对于范围较广的游戏创建或精品迭代，全部五个都加载。不要仅仅因为本总监已包含一份精简的阶段 OS 就跳过同级加载。

## 外部资产来源关卡

当上述触发类别存在时，在加载相关技能文件之前，不要断定「不需要 3D 生成器」「不需要图像生成器」或「不需要音频生成器」。

在声称某个 API 密钥不可用之前，运行凭据探测并把它的原始输出粘贴到报告中：

```bash
bash <director-skill-dir>/scripts/probe_asset_credentials.sh
```

预期输出形态：

```text
TRIPO_API_KEY=SET|MISSING
GEMINI_API_KEY=SET|MISSING
ELEVENLABS_API_KEY=SET|MISSING
```

该探测会加载用户的 shell 配置文件，只打印 SET/MISSING 标记，绝不打印密钥值。除非展示了此探测输出，否则「密钥不可用」不是有效的跳过理由。

对于范围较广或精品的游戏工作，在画质阶段之前创建一份资产来源台账：

```text
外部资产来源：
- 凭据探测输出：
- 英雄/玩家：
- 敌人/载具/武器：
- 标志性道具/拾取物：
- 世界/天空/背景：
- 材质/纹理/贴花：
- Logo/图标/GUI 美术：
- 每个表面选定的来源：程序化 / threejs-image-generator / threejs-3d-generator / 混合
- 3D 生成器已加载：是/否，路径或阻碍：
- 图像生成器已加载：是/否，路径或阻碍：
- 音频生成器已加载：是/否/不需要，路径或阻碍：
- 已生成外部资产：是/否，产物或理由：
- 已生成音频资产：是/否/不需要，产物或理由：
```

加载技能之后允许跳过实际外部生成的理由：

- 用户明确要求不使用外部 AI/资产，或仅要离线产物。
- 凭据探测输出显示相关密钥为 `MISSING`。
- 在尝试生成命令之后发生了真实的 API/网络/配额错误；附上命令和错误摘要。
- 该表面是重复出现的低价值道具，更适合用实例化/程序化套件处理。
- 某个非英雄级的重复/辅助表面在视觉评分卡中已得 2 分以上，且资产来源台账解释了为何外部生成不会改善当前截图。

如果游戏包含载具、飞船、角色、生物、武器、建筑、天空/背景美术、Logo/图标、贴花、GUI 美术或音频/SFX/配音需求，那么在相关生成器技能已被加载且资产来源台账解释了权衡之前，`不需要` 不是有效的台账条目。对于 premium 声称，除非有允许的跳过理由构成阻碍，至少一个高价值视觉资产表面应当使用 `threejs-image-generator`、`threejs-3d-generator` 或有记录的混合方案。

对于带英雄级表面（如玩家、敌人、Boss、生物、载具、飞船、武器、建筑或标志性道具）的 premium 声称，除非凭据探测或尝试生成显示了真实阻碍，否则仅用程序化不是允许的最终答案。至少一个英雄/高价值资产必须有真实的外部证据：一个 3D 生成器任务 ID、下载的 GLB/GLTF/FBX 路径、图像生成器输出路径，或有记录的混合链路。对于包含活跃玩法的 premium 声称，除非用户明确要求静音/离线产物或 `ELEVENLABS_API_KEY` 被阻断，否则仅省略音频必须作为遗留缺口上报。

## 强制参考文件关卡

参考文件不是可选的补充，而是阶段进入关卡。对于范围较广的游戏创建、premium/AAA/showcase/打磨类请求、release-ready 工作，或任何声称高视觉质量的任务，在该阶段实现之前加载适用的参考文件。

必需的阶段参考文件：

- 玩法系统：`threejs-gameplay-systems/references/gameplay-workflows.md`
- 物理选型，当玩法涉及大量物理/碰撞时：`threejs-gameplay-systems/references/physics-engine-selection.md`
- 新游戏完成清单，当创建游戏或首个可玩切片时：`threejs-gameplay-systems/references/checklists/new-game-definition-of-done.md`
- 无尽跑酷清单，当构建或升级无尽跑酷时：`threejs-gameplay-systems/references/checklists/endless-runner-premium-quality.md`
- AAA 画质：`threejs-aaa-graphics-builder/references/visual-scorecard.md`
- AAA 画质：`threejs-aaa-graphics-builder/references/implementation-blueprint.md`
- AAA 画质：`threejs-aaa-graphics-builder/references/model-recipes.md`
- AAA 画质：`threejs-aaa-graphics-builder/references/render-recipes.md`
- AAA 画质清单，用于 premium/AAA/showcase 声称：`threejs-aaa-graphics-builder/references/checklists/aaa-game-quality-gate.md` 和 `threejs-aaa-graphics-builder/references/checklists/aaa-visual-scorecard.md`
- UI：`threejs-game-ui-designer/references/ui-patterns.md`
- UI 清单，当涉及 UI/HUD/菜单/触控布局时：`threejs-game-ui-designer/references/checklists/game-ui-quality.md`、`threejs-game-ui-designer/references/checklists/hud-readability.md` 和 `threejs-game-ui-designer/references/checklists/responsive-ui-fit.md`
- 调试/性能分析：`threejs-debug-profiler/references/debug-profile-checklists.md`
- 调试/性能分析清单，当调试或做性能分析时：`threejs-debug-profiler/references/checklists/scene-debugging.md` 或 `threejs-debug-profiler/references/checklists/performance-profile.md`
- QA/release：`threejs-qa-release/references/qa-release-checklists.md`
- QA/release 清单，用于最终核验：`threejs-qa-release/references/checklists/visual-verification.md`、`threejs-qa-release/references/checklists/playtest-qa.md` 和 `threejs-qa-release/references/checklists/release.md`
- 3D 生成器，当被外部资产来源关卡加载时：`threejs-3d-generator/references/api-notes.md`
- 3D 生成器，当为游戏加载时：`threejs-3d-generator/references/threejs-integration.md`
- 3D 加图像生成器，当两者都被加载时：`threejs-3d-generator/references/image-generator-workflows.md`
- 音频生成器，当为游戏加载时：`threejs-audio-generator/references/audio-workflows.md`

提示词模板打包在总监及相关同级技能下的 `references/prompt-templates.md` 中。仅当用户要求可复用的提示词或任务模板时才加载它们。

按以下顺序尝试参考文件路径：

1. 相对于已加载技能路径：`<loaded-skill-dir>/references/<file>.md`
2. Claude 默认路径：`~/.claude/skills/<skill-name>/references/<file>.md`
3. Codex 默认路径：`~/.codex/skills/<skill-name>/references/<file>.md`
4. 通用 agents 路径：`~/.agents/skills/<skill-name>/references/<file>.md`
5. 仓库源码路径：`skills/<skill-name>/references/<file>.md`

规则：

- 在阶段进入时加载参考文件，而非在末尾。
- 在参考文件台账中追踪每一个必需参考文件，标注是/否、路径和失败理由。
- 在其必需参考文件加载完成之前，或在最终答案明确报告参考文件不可用且该阶段为阻塞/回退之前，某个阶段不能标记为 `done`。
- 对于 premium/AAA/showcase 声称，最终回复必须包含来自 `visual-scorecard.md` 的、填好的 10 类视觉评分卡，含平均分和仍存在的自动失败项。
- 对于范围较广的工作，附上每个相关参考文件的阶段清单产出，而不只是一句「游戏能跑」的总结。
- 对于范围较广、premium、AAA、showcase、完整和 release-ready 类请求，默认走充分模式（thorough）。仅对不声称精品质量的窄范围修复才允许经济模式（economy）。

如果有 Task/子智能体/工作流工具可用，把每个主要阶段委派给一个专注的 worker，并显式加载该阶段的 `SKILL.md` 及其必需参考文件。如果这些工具不可用，在加载了同样的参考文件之后串行执行。

## 台账

同时追踪技能加载与阶段执行：

- 总监：活跃
- 已加载同级技能：
  - 玩法系统：是/否，路径或理由：
  - AAA 画质：是/否，路径或理由：
  - UI：是/否，路径或理由：
  - 调试/性能分析：是/否，路径或理由：
  - QA/release：是/否，路径或理由：
  - 3D 生成器：是/否/不需要，路径或理由：
  - 图像生成器：是/否/不需要，路径或理由：
  - 音频生成器：是/否/不需要，路径或理由：
- 外部资产来源：
  - 凭据探测输出：
  - 英雄/玩家来源：
  - 敌人/载具/武器来源：
  - 标志性道具/拾取物来源：
  - 世界/天空/背景来源：
  - 材质/纹理/贴花来源：
  - Logo/图标/GUI 美术来源：
  - 音频/SFX/配音来源：
  - 已生成外部资产或跳过理由：
  - 已生成音频资产或跳过理由：
- 已加载必需参考文件：
  - 玩法工作流：是/否/不需要，路径或理由：
  - 物理引擎选型：是/否/不需要，路径或理由：
  - 玩法/新游戏清单：是/否/不需要，路径或理由：
  - 视觉评分卡：是/否/不需要，路径或理由：
  - 画质实现蓝图：是/否/不需要，路径或理由：
  - 模型配方：是/否/不需要，路径或理由：
  - 渲染配方：是/否/不需要，路径或理由：
  - 画质清单：是/否/不需要，路径或理由：
  - UI 模式：是/否/不需要，路径或理由：
  - UI 清单：是/否/不需要，路径或理由：
  - 调试/性能分析清单：是/否/不需要，路径或理由：
  - QA/release 清单：是/否/不需要，路径或理由：
  - 3D 生成器 API 说明：是/否/不需要，路径或理由：
  - 3D 生成器 Three.js 集成：是/否/不需要，路径或理由：
  - 3D/图像生成器工作流：是/否/不需要，路径或理由：
  - 音频工作流：是/否/不需要，路径或理由：
- 玩法系统：待定/进行中/已完成/已跳过，证据：
- 外部资产来源：待定/进行中/已完成/已跳过，证据：
- AAA 画质：待定/进行中/已完成/已跳过，证据：
- UI：待定/进行中/已完成/已跳过，证据：
- 调试/性能分析：待定/进行中/已完成/已跳过，证据：
- QA/release：待定/进行中/已完成/已跳过，证据：

只有同时具备实现与核验证据，某个阶段才算完成。

## 阶段路由

- `threejs-gameplay-systems`：首个可玩切片、架构、机制、实体、输入、相机、操控、游戏手感。
- 物理选型：引擎选择、固定时间步、碰撞体策略、传感器、碰撞代理、CCD、诊断，以及物理密集型游戏的 QA。
- 外部资产来源：凭据探测、生成器技能加载、资产来源决策、任务 ID/输出文件或阻碍证据。对于精品画质工作，此阶段必须在 `threejs-aaa-graphics-builder` 能被标记为完成之前完成。
- `threejs-aaa-graphics-builder`：基础感的截图、资产架构、模型、材质、VFX、灯光/渲染、视觉评分卡。
- `threejs-game-ui-designer`：HUD、菜单、覆盖层、响应式 UI、图标、安全区、UI 状态。
- `threejs-debug-profiler`：空白画布、渲染/运行时 bug、加载、缩放、移动端输入/渲染 bug、性能分析。
- `threejs-qa-release`：浏览器 QA、截图、画布像素、响应式检查、生产构建、预览、发布说明。
- `threejs-3d-generator`：外部 AI 生成的模型、GLB/FBX 输出、文本/图像生 3D、纹理、自动骨骼绑定、动画、格式转换。
- `threejs-image-generator`：2D 概念/参考图、图生模型的输入、纹理、天空/背景、Logo、图标、GUI 元素、贴花。
- `threejs-audio-generator`：生成的 SFX、循环环境音、UI 音效、配音/TTS、音色转换、清理/分离，以及游戏音频运行时规划。

如果某个同级技能文件已加载，就按其工作流执行该阶段。如果不可用，记录缺失的路径/理由，并对该阶段使用 `references/director-phase-os.md`。

## 打包的运行时资源

对于新项目，使用玩法技能打包的脚手架创建器：

```bash
python3 <threejs-gameplay-systems-skill-dir>/scripts/create_threejs_game.py ./my-game
```

对于画布检查，可用时使用生成的游戏的 `npm run inspect:canvas`，或使用 QA 技能打包的检查器：

```bash
node <threejs-qa-release-skill-dir>/scripts/inspect-threejs-canvas.mjs --url http://127.0.0.1:5188
```

## 精品完成规则

对于 premium、AAA、精修、完整、release-ready 或 showcase 类请求，完成要求在以下各方面都有可见的质量：玩法、英雄/玩家、障碍/敌人、奖励/可交互物、世界套件、HUD/菜单状态、渲染/灯光/材质、手感、性能/移动端，以及 QA。

如果截图被基本几何体、扁平道路/竞技场、通用数值卡片、稀疏世界或仅靠辉光的细节主导，任务就没有完成。

评分卡必须使用来自 `threejs-aaa-graphics-builder/references/visual-scorecard.md` 的确切类别：艺术指导、英雄/玩家、障碍/敌人、奖励/可交互物、世界/环境、材质/纹理、灯光/渲染、VFX/动效、UI/HUD，以及性能证据。不要用个人自拟的评分标准替代。

## 必需的核验

- 构建/类型检查。
- 本地浏览器运行。
- 控制台/页面错误检查。
- 活跃状态下的桌面端与移动端截图。
- 非空白画布的像素证据。
- 主要输入/目标/失败或重开路径。
- 用于 premium/AAA 声称的视觉评分卡。
- 用于 premium/AAA 或非基础画质声称的外部资产来源台账。
- 用于 premium/AAA 资产类别声称的凭据探测输出与真实外部资产产物或阻碍证据。
- 用于 premium 活跃玩法声称的音频矩阵/生成音频证据，或已上报的阻碍。
- 画质变更时的渲染器诊断。
- 带证据与遗留阻碍的最终台账。

## 报告审计

当 shell 工具可用时，把最终证据报告草拟到一个临时 markdown 文件，并在定稿范围较广或精品的工作之前运行总监审计：

```bash
python3 <director-skill-dir>/scripts/audit_reference_report.py --premium /path/to/final-report.md
```

对 premium、AAA、showcase、high-fidelity、精修、完整、release-ready 或「非基础」声称使用 `--premium`。对物理密集型游戏（如台球/斯诺克、迷你高尔夫、弹珠台、弹珠竞速、物理解谜、刚体游戏，或带许多传感器/碰撞体的游戏）追加 `--physics`。当涉及生成或集成音频时追加 `--audio`，并且对 premium 活跃玩法声称也追加，除非用户要求静音/仅离线产物。如果审计失败，修复缺失的报告小节，或说明确切的阻碍，而不是声称完成。如果脚本不可用，手动强制执行同样的必需小节：技能加载台账、参考文件台账、外部资产/音频来源台账、阶段清单、视觉评分卡、相关时的物理/音频诊断、核验证据，以及遗留风险。

## 最终回复

报告技能加载台账、参考文件台账、外部资产来源台账、阶段台账、变更的文件、运行 URL、操控方式、核验命令、截图/产物、渲染器/性能说明、已通过的质量关卡、已跳过的阶段，以及遗留风险。对于 premium/AAA/showcase 声称，附上填好的视觉评分卡与仍存在的自动失败项。用词要精确：「调用（invoked）」指一次斜杠/工具技能调用；「加载（loaded）」指 `SKILL.md` 或参考文件已被读入上下文；「执行阶段（executed phase）」指工作是在已加载技能的指引或总监回退方案之下完成的。
