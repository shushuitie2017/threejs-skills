---
name: threejs-3d-generator
description: "使用 Tripo API 为 Three.js 游戏生成、贴纹理、绑骨骼、做动画、风格化、转换并下载 3D 资产。适用于 text-to-3D、image-to-3D、2D 概念图转 3D、可直接用于游戏的 GLB/FBX 资产、角色、生物、建筑、道具、武器、地形块、auto-rigging、动画重定向、模型 texturing、LEGO/voxel/Minecraft 风格化、low-poly/quad 转换以及浏览器资产管线。在 image-to-3D 生成前，可与 threejs-image-generator 搭配，用于概念图、texture 参考、天空/背景/地形 texture、logo、图标和 GUI 美术。"
---

# Three.js 3D Generator

## 用途

先创建面向生产的 3D 资产，再把它们准备好接入 Three.js 游戏。这是 Three.js 游戏系统的 3D 生成层，使用 Tripo 作为 text-to-3D、image-to-3D、texturing、rigging、重定向、风格化、转换以及可下载 GLB/FBX 输出的供应商。

## API 密钥

绝不要把 API 密钥存进技能文件或客户端游戏代码里。脚本按以下顺序检查：

1. `--api-key`
2. `TRIPO_API_KEY`

在断定密钥不可用之前，先执行第 0 步：

```bash
bash ~/.claude/skills/threejs-game-director/scripts/probe_asset_credentials.sh
```

对于 Codex 安装：

```bash
bash ~/.codex/skills/threejs-game-director/scripts/probe_asset_credentials.sh
```

把 `TRIPO_API_KEY=SET|MISSING` 的原始输出粘贴到报告里。在这个凭据探测把用户的 shell 配置文件加载进来之前，不要仅凭一个普通的非交互式 shell 就断定密钥不可用。

当探测显示 SET 但 `threejs_3d_asset.py` 报告密钥缺失时，说明密钥是在一个仅交互式的配置文件里导出的（例如 `~/.zshrc`）。此时用和探测脚本相同的方式包裹脚本调用：

```bash
zsh -c 'source "$HOME/.zprofile" 2>/dev/null; source "$HOME/.zshrc" 2>/dev/null; python3 .../threejs_3d_asset.py ...'
```

只在本地/服务器端工具中使用该 API。生成的模型下载 URL 很快就会过期，所以任务成功后要立即下载输出。

## 工具脚本

参考文档闸门：

- 在做供应商 API 相关工作、端点/任务决策、模型版本选择、轮询、后处理、转换、rigging、animation 或下载处理之前，先加载 `references/api-notes.md`。
- 在把 Tripo 输出导入浏览器游戏或就 GLB/FBX 集成给出建议之前，先加载 `references/threejs-integration.md`。
- 在把 `threejs-image-generator` 与本技能搭配用于 2D 概念图、texture 参考、UI 美术、logo、贴花或 image-to-3D 输入之前，先加载 `references/image-generator-workflows.md`。

用一个参考文档台账跟踪必读的参考文档，记录 yes/no、路径和失败原因。只要还有必读参考文档被跳过，就不要把资产管线标记为完成。

从用户当前的项目目录运行：

```bash
python3 ~/.claude/skills/threejs-3d-generator/scripts/threejs_3d_asset.py --help
```

如果安装在 Codex 而非 Claude，则用：

```bash
python3 ~/.codex/skills/threejs-3d-generator/scripts/threejs_3d_asset.py --help
```

## 常用命令

推荐的高品质游戏核心模型：

```bash
python3 ~/.claude/skills/threejs-3d-generator/scripts/threejs_3d_asset.py text \
  --prompt "game-ready [hero asset], strong readable silhouette, layered hard-surface detail, PBR materials, clean topology for browser game, centered pivot, 3/4 view, no text" \
  --model-version v3.1-20260211 \
  --texture-quality detailed \
  --geometry-quality detailed \
  --wait --download --out-dir assets/models/hero
```

Text to 3D：

```bash
python3 ~/.claude/skills/threejs-3d-generator/scripts/threejs_3d_asset.py text \
  --prompt "game-ready sci-fi hover bike, sleek armored panels, readable silhouette, PBR, front facing" \
  --model-version v3.1-20260211 \
  --texture-quality detailed \
  --geometry-quality detailed \
  --wait --download --out-dir assets/models/hover-bike
```

从本地 `threejs-image-generator` 概念图做 Image to 3D：

```bash
python3 ~/.claude/skills/threejs-3d-generator/scripts/threejs_3d_asset.py image \
  --image assets/concepts/hover-bike-front.png \
  --model-version v3.1-20260211 \
  --enable-image-autofix \
  --texture-alignment original_image \
  --texture-quality detailed \
  --wait --download --out-dir assets/models/hover-bike
```

查询状态与下载：

```bash
python3 ~/.claude/skills/threejs-3d-generator/scripts/threejs_3d_asset.py status TASK_ID
python3 ~/.claude/skills/threejs-3d-generator/scripts/threejs_3d_asset.py download TASK_ID --out-dir assets/models
```

贴纹理、绑骨骼、做动画或转换：

```bash
python3 ~/.claude/skills/threejs-3d-generator/scripts/threejs_3d_asset.py postprocess \
  --type texture_model --original-task-id TASK_ID \
  --texture-prompt "brushed gunmetal, orange hazard decals, worn edges" \
  --wait --download --out-dir assets/models/retextured

python3 ~/.claude/skills/threejs-3d-generator/scripts/threejs_3d_asset.py postprocess \
  --type animate_prerigcheck --original-task-id TASK_ID --wait

python3 ~/.claude/skills/threejs-3d-generator/scripts/threejs_3d_asset.py postprocess \
  --type animate_rig --original-task-id TASK_ID --rig-type biped --spec tripo --wait

# animate_retarget 接收的是 RIG 任务 ID，而不是生成任务 ID。
# 通过 --animations 每个任务最多批量处理 5 个预设。
# 绝不要传 --animate-in-place：它会破坏烘焙（肢体镜像 / 蒙皮炸裂）。
# 应改在引擎里剥除 root motion。
python3 ~/.claude/skills/threejs-3d-generator/scripts/threejs_3d_asset.py postprocess \
  --type animate_retarget --original-task-id RIG_TASK_ID --model-version v2.5-20260210 \
  --animations preset:idle,preset:walk,preset:run \
  --wait --download --out-dir assets/models/animated

python3 ~/.claude/skills/threejs-3d-generator/scripts/threejs_3d_asset.py postprocess \
  --type conversion --original-task-id TASK_ID --format GLTF \
  --face-limit 20000 --wait --download --out-dir assets/models/gltf

python3 ~/.claude/skills/threejs-3d-generator/scripts/threejs_3d_asset.py postprocess \
  --type stylize_model --original-task-id TASK_ID --style voxel \
  --wait --download --out-dir assets/models/voxel
```

动画角色管线（生成 -> prerigcheck -> 带重试的已验证 rig -> 重定向 -> 下载）。管线会根据身体结构自行路由：双足角色自动使用 v1.0-20240301 解剖学 rig，每个动画一个 FBX（普通预设名会映射到 preset:biped:* 库）；生物则使用 v2.5-20260210 rig 配 GLB 片段：

```bash
python3 ~/.claude/skills/threejs-3d-generator/scripts/threejs_3d_asset.py character-pipeline \
  --prompt "stylized cyber runner character, T-pose, full body, game-ready outfit, readable silhouette" \
  --animations preset:idle,preset:walk,preset:run,preset:jump \
  --out-dir assets/models/cyber-runner

# 生物示例：站姿的表达很关键——按预设期望的姿势去生成。
python3 ~/.claude/skills/threejs-3d-generator/scripts/threejs_3d_asset.py character-pipeline \
  --prompt "stylized wolf, quadrupedal stance, all four legs planted and separated, full body" \
  --rig-type quadruped --animations preset:quadruped:walk \
  --out-dir assets/models/wolf
```

## 与 Three.js Image Generator 的搭配

当资产能受益于一张强有力的 2D 参考时，在 3D 生成之前先用 `threejs-image-generator`：

- 角色概念图、全身 T-pose/A-pose、正面/侧面/背面变体。
- 建筑、道具、载具、武器、拾取物、敌人、障碍物或地形块参考。
- 整个资产家族的风格表。
- Texture 参考：地形、岩石、金属、织物、贴花、天空盒、背景、UI 材质。
- Logo、阵营标记、拾取物图标、危险标志、座舱贴花、HUD 符号和 GUI 面板。

在生成或编辑 2D 输入之前，加载 `references/image-generator-workflows.md` 获取提示词模式。

## Three.js 集成

在把 Tripo 输出导入浏览器游戏之前，先加载 `references/threejs-integration.md`。简而言之：

- 对 Three.js 优先使用 GLB/PBR 输出。
- 用 `GLTFLoader` 加载。
- 对已绑骨骼/带动画的 GLB 使用 `AnimationMixer`。
- 让生成的模型文件远离客户端 API 流程；生成只是一个工具环节。
- 检查三角面数、texture 数量、材质数量、文件大小、缩放、pivot、包围盒和动画片段。
- 把生成的 3D 资产用作核心/高精内容，再用 procedural 方式或额外几轮 `threejs-3d-generator` / `threejs-image-generator` 来搭建周边的道具套件。

## 骨骼绑定与动画的可靠性

加载 `references/api-notes.md` 获取完整的参数表。以下规则能避免大多数失败：

- 把角色生成为一个融合的整体 mesh：让 `--quad` 和 `--generate-parts` 保持关闭（`generate_parts` 会禁用 texturing；`quad` 会强制输出 FBX）。
- 要求全身 T-pose 或 A-pose，双臂远离身体、左右对称、没有道具融进轮廓里。在 rigging 之前先确认渲染预览确实处于 T/A-pose；不是的话就重新生成。
- 先运行 `animate_prerigcheck`（它不接收模型版本），并用它检测出的 `rig_type` 来做 `animate_rig` 和选预设。`riggable=false` 意味着换个更清晰的姿势重新生成，而不是强行绑骨骼。
- `riggable=true` 并不保证 rig 可用。绑骨骼后，在重定向之前先验证骨架：`threejs_3d_asset.py validate-rig rig-model.glb --rig-type biped`（`character-pipeline` 会自动做这一步）。既要检查存在性也要检查链深：一条只有 1 根骨头的腿或 2 根骨头的手臂会扭曲每个片段。
- Auto-rigging 是非确定性的。验证失败时，先重试 rig 任务（约 25 credits）再考虑重新生成模型——`character-pipeline --rig-retries N`（默认 2）会自动化这一步，`--model-task-id TASK_ID` 可从已有的生成结果续跑。带盔甲/硬表面的角色需要最多的重试；有机 mesh 通常一次就能绑好。
- 生物只有恰好一个预设（walk/march）。对多运动模式的生物（会爬又会飞的龙），给同一个模型绑两次骨骼——用地面 rig 类型对应移动预设，用 `avian` 对应翅膀链——并在 Three.js 里用 procedural 方式驱动翅膀，或通过 `mixamo` 规格 rig 上的外部片段来驱动。
- 重定向后的片段按请求顺序命名为 `NlaTrack`、`NlaTrack.001`……——按索引映射，导入后再重命名。
- Rig 版本是主要的质量杠杆，且随身体结构不同而不同（2026 年 6 月实测）。`character-pipeline` 会自动路由；只有在你有意为之时才覆盖 `--rig-model-version`：
  - 人形（HUMANOIDS）：`v1.0-20240301`（类似 Mixamo 的解剖学骨架，带 twist bone + 庞大的 `preset:biped:*` 片段库：idle、walk、run、slash、jump、dances……）。v2.x 的肢链 rigger 在人形 mesh 上 0/16 全败——不管有没有盔甲、T-pose 还是 A-pose——总是产出不对称的链。
  - 生物（CREATURES）：`v2.5-20260210`（v2.x 对四足/鸟类处理得很好：对称的 5-6 根骨头链）。
- 对 v1.0 rig，用 `--model-version default` 做重定向（省略版本）：重定向的枚举会拒绝显式的 `v1.0-20240301`（HTTP 400 code 2017），但服务器默认值能正确处理 v1.0 rig。
- v1.0 重定向必须用 `--out-format fbx`（脚本会强制这一点）：Tripo 在这条路径上的 GLB 烘焙会把 twist-bone 变换导到错误的空间，肢体会塌进躯干——同一个任务的 FBX 是正确的。用 three.js 的 `FBXLoader` 加载或离线转换。v2.5 生物重定向做成 GLB 没问题。
- 当 Tripo 预设要被重定向时，使用 `--spec tripo`（默认值）；`--spec mixamo` 的 rig 不能用于 Tripo 重定向，只用于外部动画管线。
- `animate_retarget` 接收的是 RIG 任务 ID。通过 `--animations` 每个任务最多批量处理 5 个预设。
- v2.5 rig 只有 16 个预设（没有 `preset:attack`；用 `preset:slash`/`preset:shoot`）。非双足 rig 类型各只有一个移动预设；额外的生物动作要用 procedural 方式或外部重定向来规划。
- 生物的 mesh 站姿决定了预设如何呈现：让一条直立站着的龙做四足行走，看起来会像人在走路。按动画期望的站姿去生成生物（身体水平、四肢着地）——管线只会为双足 rig 自动追加 T-pose 措辞。
- 下载后，运行 `threejs_3d_asset.py validate-animation clip.glb`（关键帧 QA：标记 scale 轨道、导致肢体拉伸的 translation 轨道、极端旋转，并报告每个片段的时长/通道覆盖），然后在引擎里目视确认动作。
- 绝不要用 `--animate-in-place`（已验证会破坏片段：v1.0 rig 上肢体镜像/交叉，v2.5 上蒙皮炸裂）。让 root motion 保持烘焙状态，在导入时再转成 in-place：只把 root 骨骼位置轨道的水平分量归零，保留垂直分量（跳跃和步态起伏都在那里）。之后由游戏逻辑代码驱动移动。确切代码片段见 `threejs-integration.md`。
- 下载后，在接线 `AnimationMixer` 之前先检查 `gltf.animations` 的片段名和数量。

## 质量规则

- 用材质、silhouette、镜头/可读性、缩放和游戏用途约束来改进用户的提示词。
- 对可绑骨骼的角色，在提示词里包含全身 T-pose 或 A-pose，或先做一张 T-pose 参考图。
- 对 Three.js 游戏，请求 GLB/PBR、合理的面数上限，以及与性能预算相匹配的 texture 质量。
- 对移动端/浏览器游戏，当资产开销太大时，优先用 `smart_low_poly`、`face_limit`、后续转换或 low-poly 后处理。
- 成功后总是立即下载输出 URL。
- 报告凭据探测输出、参考文档台账、任务 ID、输出路径、模型版本、texture/geometry 设置、animation、转换设置、Three.js 导入注意事项，以及任何缺失/失败的步骤。
