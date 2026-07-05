---
name: threejs-audio-generator
description: "使用 ElevenLabs 为 Three.js 浏览器游戏生成、转换、清理并准备音频资产。适用于音效（SFX）、循环环境音、界面音、打击/武器/载具音效、生物或 Boss 出场音（stinger）、解说语音/对白 TTS、以草稿演出为源的变声、音频降噪清理与人声隔离、音频清单，以及可直接用于 Web 的游戏音频集成。"
---

# Three.js Audio Generator

## 用途

为 Three.js 项目制作可直接用于游戏的音频资产。本技能把游戏音效生成、语音生成/转换、音频降噪清理、凭据探测和运行时集成整合到一套专注于 Three.js 的生产流程中。

提供方：ElevenLabs。

## 何时使用

在以下场景使用本技能：

- 音效（SFX）：跳跃、打击、武器、爆炸、金币、拾取、碰撞、界面点击、确认、报错。
- 环境音：风、雨、城市底噪、引擎嗡鸣、传送门循环、地牢房间氛围、战斗竞技场底音。
- 语音：解说短语、Boss 台词、教学提示、菜单旁白、生成的占位对白。
- 变声：把一段草稿演出转换成目标角色的声音，同时保留时序与情感。
- 降噪清理：在变声、TTS 替换或转录之前隔离人声或去噪对白。
- Three.js 集成：Web Audio 加载、循环、精灵表/清单映射、音量分组、暂停/恢复、用户手势解锁。

对于高端/3A/展示级游戏工作，音频不是可有可无的装饰。除非用户明确要求静音/仅离线输出，或凭据/API 尝试被阻断，否则至少为主循环生成或集成一套最小的交互音频。

## API Key

绝不要把 API 密钥存放在技能文件或浏览器/游戏代码中。脚本会依次检查：

1. `--api-key`
2. `ELEVENLABS_API_KEY`

在 `threejs-game-director` 工作流中宣布密钥不可用之前，先运行 director 凭据探测，并原样粘贴其输出的 SET/MISSING 结果：

```bash
bash ~/.codex/skills/threejs-game-director/scripts/probe_asset_credentials.sh
```

Claude 安装环境：

```bash
bash ~/.claude/skills/threejs-game-director/scripts/probe_asset_credentials.sh
```

如果探测显示 `ELEVENLABS_API_KEY=SET` 但脚本却读不到密钥，请通过一个会加载用户 profile 的 shell 来运行：

```bash
zsh -c 'source "$HOME/.zprofile" 2>/dev/null; source "$HOME/.zshrc" 2>/dev/null; python3 ~/.codex/skills/threejs-audio-generator/scripts/threejs_audio_asset.py probe'
```

## 必读参考

在制定游戏音频方案、生成多个资产、接入运行时音频、清理/转换人声，或声称已完成高端游戏音频之前，先加载 `references/audio-workflows.md`。

在参考文献台账中登记它。在跳过该参考的情况下，不要把音频阶段标记为完成。

## 工具脚本

在用户当前的游戏项目目录下运行：

```bash
python3 ~/.codex/skills/threejs-audio-generator/scripts/threejs_audio_asset.py --help
```

Claude 安装路径：

```bash
python3 ~/.claude/skills/threejs-audio-generator/scripts/threejs_audio_asset.py --help
```

探测：

```bash
python3 ~/.codex/skills/threejs-audio-generator/scripts/threejs_audio_asset.py probe
```

生成音效（SFX）：

```bash
python3 ~/.codex/skills/threejs-audio-generator/scripts/threejs_audio_asset.py sfx \
  --prompt "tight futuristic boost pickup, bright transient, short sparkling tail, arcade racing game" \
  --duration 1.2 \
  --prompt-influence 0.65 \
  --out assets/audio/sfx/boost-pickup.mp3
```

生成循环环境音：

```bash
python3 ~/.codex/skills/threejs-audio-generator/scripts/threejs_audio_asset.py sfx \
  --prompt "seamless cyber resort mini golf ambience, distant surf, soft neon transformer hum, gentle crowd bed" \
  --duration 12 \
  --loop \
  --prompt-influence 0.45 \
  --out assets/audio/ambience/cyber-resort-loop.mp3
```

生成 TTS/解说语音：

```bash
python3 ~/.codex/skills/threejs-audio-generator/scripts/threejs_audio_asset.py tts \
  --text "Perfect shot." \
  --voice-id JBFqnCBsd6RMkjVDRZzb \
  --out assets/audio/voice/perfect-shot.mp3
```

清理对白：

```bash
python3 ~/.codex/skills/threejs-audio-generator/scripts/threejs_audio_asset.py isolate \
  --input assets/audio/source/noisy-boss-line.wav \
  --out assets/audio/voice/boss-line-clean.mp3
```

把草稿演出转换成目标声音：

```bash
python3 ~/.codex/skills/threejs-audio-generator/scripts/threejs_audio_asset.py voice-change \
  --input assets/audio/source/scratch-boss-line.wav \
  --voice-id JBFqnCBsd6RMkjVDRZzb \
  --remove-background-noise \
  --out assets/audio/voice/boss-line-final.mp3
```

## 游戏音频默认参数

- 音效（SFX）：`mp3_44100_128`，0.5-2.5 秒，prompt influence `0.55-0.8`。
- 界面音：0.15-0.8 秒，高 prompt influence，保持瞬态清晰。
- 环境音循环：8-30 秒，`--loop`，prompt influence `0.3-0.55`。
- 语音：干净的生成台词用 TTS；当时序/表演源自草稿演出且很重要时用变声。
- 降噪清理：在变声或最终对白使用之前，先隔离带噪语音。
- 运行时：本地生成、提交/导入文件，并通过 Web Audio/Three.js 集成加载它们。绝不要把 API 密钥放进浏览器代码。

## 必交报告

报告内容：

- 凭据探测输出或真实的阻断原因。
- 参考文献台账。
- 生成/处理后的文件路径。
- 提示词/文本/输入文件、voice ID、时长、循环标志与输出格式。
- 运行时集成说明：音频分组、触发事件、循环行为、解锁手势、暂停/恢复、音量/静音控制。
- 尚存的音频缺口，以及与用户 ElevenLabs 账户相关的任何授权/套餐假设。
