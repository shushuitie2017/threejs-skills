---
name: threejs-image-generator
description: "使用 Google 的 Gemini 图像 API 为 Three.js 游戏生成并编辑 2D 图像资产。适用于概念原画表、图生 3D 输入、纹理（texture）参考、天空/背景板、贴花（decal）、标识、图标、界面美术（GUI art）、标题/菜单美术、缩略图、营销静帧，以及供给 threejs-3d-generator 的源图像。当用户提供图像路径时，也可用于直接的图像编辑。"
---

# Three.js Image Generator

## 用途

为 Three.js 项目制作可用于游戏的 2D 资产与参考图。本技能是 Three.js 游戏系统的图像生成层：它产出概念图、纹理、贴花、界面美术和 2D 输入，可交给 `threejs-3d-generator` 用于图生 3D 建模。

提供方：Google 的 Gemini 图像 API。

## 何时使用

在仅走程序化（procedural）回退方案之前，当 Three.js 游戏需要以下内容时，先使用本技能：

- 供 `threejs-3d-generator` 使用的 2D 转 3D 参考图：角色、生物、建筑、飞船、汽车、武器、道具、拾取物、地形模块。
- 纹理与材质参考：地形、道路、岩石、沙地、金属、科幻面板、trim sheet、贴花、危险标签、标牌。
- 环境图：天空、背景、城市天际线、星云板、菜单背景、视差层。
- 界面美术：标识、阵营徽记、图标、物品卡、技能徽章、座舱贴花、GUI 面板、标题美术。
- 对已有图像的编辑、风格变体、清理、配色对齐，或概念原画表的细化。

对于高端/3A/展示级图形工作，除非凭据探测或一次真实的生成尝试显示存在阻断，否则至少为高价值的 2D 表面或图生 3D 输入生成一张相关图像。

## API Key

绝不要把 API 密钥存放在技能文件或浏览器/游戏代码中。脚本会依次检查：

1. `--api-key`
2. `GEMINI_API_KEY`

在 `threejs-game-director` 或 `threejs-aaa-graphics-builder` 工作流中宣布密钥不可用之前，先运行 director 凭据探测，并原样粘贴其输出的 SET/MISSING 结果：

```bash
bash ~/.codex/skills/threejs-game-director/scripts/probe_asset_credentials.sh
```

Claude 安装环境：

```bash
bash ~/.claude/skills/threejs-game-director/scripts/probe_asset_credentials.sh
```

如果探测显示 `GEMINI_API_KEY=SET` 但脚本却读不到密钥，请通过一个会加载用户 profile 的 shell 来运行：

```bash
zsh -c 'source "$HOME/.zprofile" 2>/dev/null; source "$HOME/.zshrc" 2>/dev/null; uv run ~/.codex/skills/threejs-image-generator/scripts/generate_image.py --prompt "..." --filename assets/concepts/example.png'
```

## 工具脚本

在用户当前的项目目录下运行，使输出落在游戏项目里：

```bash
uv run ~/.codex/skills/threejs-image-generator/scripts/generate_image.py --prompt "your image description" --filename assets/concepts/output.png --resolution 2K
```

Claude 安装路径：

```bash
uv run ~/.claude/skills/threejs-image-generator/scripts/generate_image.py --prompt "your image description" --filename assets/concepts/output.png --resolution 2K
```

编辑一张已有图像：

```bash
uv run ~/.codex/skills/threejs-image-generator/scripts/generate_image.py \
  --input-image assets/concepts/ship.png \
  --prompt "turn this into a battle-worn red racing livery with clearer material zones" \
  --filename assets/concepts/ship-red-livery.png \
  --resolution 2K
```

分辨率映射：

- `1K`：快速概念、图标、草稿表。
- `2K`：图生 3D、纹理、背景、界面面板的默认生产参考。
- `4K`：主视觉启动图/标题美术、高细节纹理参考、大幅天空/背景板。

## 提示词模式

图生 3D 参考：

```text
Create a clean 3D-generation reference image of [asset]. Centered single object, full object visible, plain light background, readable silhouette, clear material zones, game-ready [genre/style], no motion blur, no cropped parts, no text.
```

可绑骨的角色/生物参考：

```text
Create a full-body [T-pose/A-pose/side-view creature] reference for 3D rigging: [details]. Symmetric stance, visible hands/feet/limbs, plain background, readable costume/anatomy layers, no weapon fused to hands.
```

纹理/材质参考：

```text
Create a seamless game texture reference for [surface]. Orthographic/top-down, PBR-friendly albedo, clear material variation, no perspective, no baked strong shadows, [style/material details].
```

标识/图标/界面美术：

```text
Create a crisp game UI [logo/icon/badge/panel] for [faction/item/ability]. Transparent-friendly silhouette, high contrast at small size, [genre styling], no tiny unreadable text.
```

天空/背景：

```text
Create a wide game background plate of [environment]. Layered depth, readable horizon, [time/weather/style], suitable behind a real-time Three.js scene, no foreground subject.
```

## Three.js 集成规则

- 把概念图与图生 3D 源图保存在 `assets/concepts/` 下。
- 把纹理、贴花、图标和 GUI 源图保存在 `assets/textures/`、`assets/decals/` 或 `assets/ui/` 下。
- 对于图生 3D，把已保存的图像路径交给 `threejs-3d-generator`，并在外部资产台账中记录这条链路。
- 不要从客户端游戏代码调用图像 API。
- 有意识地把生成的 PNG 转换为运行时格式：带 alpha 的/界面用 PNG，项目管线支持时较大的不透明纹理用 JPG/WebP/KTX2。
- 不仅要确认文件存在，还要验证图像在游戏中的实际呈现效果。

## 必交报告

报告内容：

- 凭据探测输出或命令阻断原因。
- 提示词与用途。
- 输出路径。
- 分辨率。
- 该图像是被直接使用、进一步编辑，还是交给了 `threejs-3d-generator`。
- 尚存的集成工作，例如压缩、UV 分配、alpha 清理或图集打包。

如果所需的图像输出缺失，而唯一的理由是「程序化已足够」，则不要把高端图形阶段标记为完成——对于高价值的界面、纹理、天空、贴花、标识或图生 3D 表面而言更是如此。
