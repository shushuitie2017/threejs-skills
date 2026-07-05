# Three.js Skills 中文版（threejs-skills）— 项目说明

Three.js 浏览器游戏开发的 **AI 技能分发包**：9 个自包含 skill（`skills/` 下），装进 Claude Code / Codex 后由 `threejs-game-director` 总监技能编排玩法/画质/UI/建模/音频/调试/质检。

## 性质与定位

- **技能分发包 + 落地页站点**——本体是 9 个自包含 skill；另有一个静态落地页（`site/` 目录）。
- **不自带成品游戏**——它是让 agent 去「造」游戏的技能，不是可玩 demo。
- 安装入口：`./install.sh --claude|--codex|--all`（本地）或 `pnpm dlx skills add shushuitie2017/threejs-skills ...`（远程）。

## 结构

```
skills/                         # 9 个 skill，各自 SKILL.md + references/ + scripts/ + assets/
  threejs-game-director/        # 总入口，编排其余
  threejs-gameplay-systems/     # 含内置 Vite+TS+Three.js 游戏脚手架 assets/threejs-vite-game/
  threejs-aaa-graphics-builder/ threejs-game-ui-designer/ threejs-debug-profiler/
  threejs-qa-release/ threejs-3d-generator/ threejs-image-generator/ threejs-audio-generator/
install.sh                      # 本地安装器（manifest = .threejs-skills-managed）
scripts/                        # 维护者校验脚本（validate-skills.sh 等）
AGENTS.md                       # Codex/agent 顶层指令（已中文化）
```

## 中文化现状（核心层已完成）

- ✅ 9 个 `SKILL.md`（frontmatter `description` + 正文）全部中文化；**`name:` 技能 ID 保留英文**（agent 靠它加载）。
- ✅ `AGENTS.md`、`README.md` 中文化。
- ⏳ 各 skill 深层 `references/`、`scripts/` 内代码注释仍为英文，按需逐步中文化。

## 维护者校验

```bash
npm install
npm run check:scripts
npm run validate:skills
```
