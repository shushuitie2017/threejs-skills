---
name: threejs-qa-release
description: "验证并发布 Three.js 浏览器游戏。整合了试玩质检、移动端/响应式检查、生产构建、预览验证、静态托管 base 路径、debug 门控、bundle 审查、截图、打包后的画布像素检查、控制台检查以及发布风险报告。"
---

# Three.js 质检/发布

## 目的

证明游戏在玩家实际遇到的形态下能正常运行，然后准备一个附带已知风险清单、可发货的浏览器构建。

## 质检工作流

在展开宽泛质检、移动端验证、bug 报告、生产预览、静态托管检查或发布准备之前，把加载 `references/qa-release-checklists.md` 作为第一步。用一张参考台账追踪它，标注是/否、路径和跳过原因。只要这份参考在质检或发布工作中被跳过，就不要把质检/发布标记为完成。

做截图/画布验证时加载 `references/checklists/visual-verification.md`，做玩法循环质检时加载 `references/checklists/playtest-qa.md`，做生产发布检查时加载 `references/checklists/release.md`。仅当用户要求可复用的质检/发布提示词或任务模板时，才加载 `references/prompt-templates.md`。

1. 如有需要，安装依赖。
2. 运行构建/类型检查。
3. 启动 dev 或 preview 服务器。
4. 打开浏览器目标页。
5. 抓取控制台/页面/网络错误。
6. 核验画布像素非空白。
7. 抓取桌面和移动端截图。
8. 触发主要输入、目标推进、失败/重试以及近期有风险的路径。
9. 检查 HUD 文字排布、安全区、触控目标、响应式布局。
10. 若音频有改动，核验用户手势解锁、SFX 触发、环境音循环的启停、暂停/重启的清理、静音/音量行为以及解码/加载错误。
11. 记录产物与问题。

## 打包的画布检查器

当目标项目本身还没有画布检查器时，使用随本技能捆绑的检查器：

```bash
node <this-skill-dir>/scripts/inspect-threejs-canvas.mjs --url http://127.0.0.1:5188
```

要做移动端模拟，加上 `--mobile`。由打包脚手架生成的游戏也自带各自的 `scripts/inspect-threejs-canvas.mjs` 和 `npm run inspect:canvas`。

## 发布工作流

1. 检查 package 脚本、Vite 配置、base 路径、public/assets。
2. 门控 debug UI/日志/测试辅助工具。
3. 运行生产构建和 preview/静态服务器。
4. 核验构建产物的桌面/移动端表现。
5. 审查 bundle 和大体积素材。
6. 记录部署命令、宿主假设和残留风险。

## 最终回复

以通过/失败开头。包含参考台账、质检矩阵/清单结果、命令、URL、操作方式、截图/产物、发现/修复的问题、部署说明和风险。
