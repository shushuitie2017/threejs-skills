---
name: threejs-debug-profiler
description: "调试 Three.js 浏览器游戏并做性能剖析。整合了场景调试，渲染/运行时/加载/动画/resize/移动端输入修复，性能剖析，draw calls，triangles，贴图，内存，shader/后处理开销，bundle 体积，以及移动端 DPR/输入问题。"
---

# Three.js 调试与性能剖析

## 目的

在不破坏可玩性的前提下，找到根因并优化实测出的瓶颈。

## 调试工作流

在调试渲染/运行时/移动端问题、素材加载、音频加载/播放、动画、resize、输入、黑屏、物理/碰撞 bug，或做性能剖析时，把加载 `references/debug-profile-checklists.md` 作为第一步。用一张参考台账追踪它，标注是/否、路径和跳过原因。只要这份参考在调试或剖析工作中被跳过，就不要把调试/剖析阶段标记为完成。

做渲染/运行时 bug 诊断时加载 `references/checklists/scene-debugging.md`，做剖析工作时加载 `references/checklists/performance-profile.md`，处理移动端渲染/输入问题时加载 `references/checklists/mobile-input.md`。仅当用户要求可复用的调试/剖析提示词或任务模板时，才加载 `references/prompt-templates.md`。

1. 在本地复现。
2. 读取控制台/页面/网络错误。
3. 检查画布显示尺寸和绘制缓冲区尺寸。
4. 检查渲染器/上下文/循环的归属。
5. 检查相机、宽高比、near/far、灯光、材质、雾、场景内容、变换。
6. 检查素材路径/加载器/CORS/base 路径。
7. 检查动画 delta 单位、物理/更新顺序、固定时间步、碰撞体/刚体归属、输入监听器、指针/触摸行为、resize，以及涉及音频时的音频上下文解锁/解码错误。
8. 在归属模块中修复根因。
9. 核验浏览器截图、画布像素非空白、控制台/页面错误和已损坏的路径。

## 性能工作流

1. 在正确的构建模式下复现。
2. 记录基线：FPS/帧时间、draw calls、triangles、几何体、贴图、内存、bundle。
3. 定位 CPU/GPU/内存/网络瓶颈。
4. 一次只优化一项：实例化、共享资源、剔除、LOD、DPR 上限、更廉价的阴影/后处理、贴图纪律。
5. 在同一场景下重新测量，并核验画面/可玩性。

## 最终回复

以根因或瓶颈开头。报告参考台账、用到的清单项、改动的文件、基线/优化后指标、命令、截图/产物、重新验证过的已损坏路径，以及残留风险。
