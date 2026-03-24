# Remotion Video Starter

[![Claude Skills](https://img.shields.io/badge/Claude-Skills-blue)](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Version](https://img.shields.io/badge/Version-2.0-purple)]()

**版本：** v2.0 | **作者：** Abu + Claude

> 🎬 一个完整的 Remotion 视频制作自动化 skill，用于快速制作产品推广视频

[English](#english) | [中文](#功能特点)

---

## ✨ 功能特点

- ✅ 自动分析 GitHub 项目并生成视频创意
- ✅ 9步完整流程，从分析到交付
- ✅ 支持竖屏（1080×1920）和横屏（1920×1080）
- ✅ 自动生成配音、发布文案、信息卡
- ✅ 支持抖音、视频号、小红书、B站、YouTube 等平台

## 🎯 适用场景

- 📦 **GitHub 项目推广视频** - 快速为开源项目制作宣传视频
- 🚀 **开源项目介绍** - 展示项目核心功能和亮点
- 💼 **产品功能演示** - B端/C端产品功能展示
- 📱 **多平台适配** - 抖音、视频号、小红书、B站、YouTube

---

## 📦 安装

### 方法 1：Git Clone（推荐）

```bash
git clone https://github.com/cuishiqing/remotion-video-starter.git ~/.claude/skills/remotion-video-starter
```

### 方法 2：使用 npx skills

```bash
npx skills add git@github.com:cuishiqing/remotion-video-starter.git
```

### 方法 3：手动下载

1. 下载 ZIP 文件
2. 解压到 `~/.claude/skills/remotion-video-starter/`

---

## 🚀 使用方法

### 基础用法

在 Claude Code 中直接说：

```
使用 remotion-video-starter skill 为 social-analyzer 制作推广视频
```

### 高级用法

**指定视频格式：**
```
为 social-analyzer 制作横屏推广视频（B站版本）
```

**指定时长：**
```
为 social-analyzer 制作60秒竖屏推广视频
```

**使用 GitHub URL：**
```
使用 remotion-video-starter skill 为 https://github.com/sherlock-project/social-analyzer 制作推广视频
```

---

## 📋 9步流程概览

## 9步流程概览

1. **Gemini 深度分析** - 理解项目核心价值
2. **设计视频结构** - 规划6场景时间线
3. **编写配音脚本** - 创作完整配音文案
4. **复制模板项目** - 快速搭建骨架
5. **更新 Remotion 配置** - 修改项目名称
6. **实现场景组件** - 实现6个场景
7. **生成配音音频** - 使用豆包TTS
8. **生成发布文案** - 视频号文案
9. **生成信息卡** - 项目封面图

详细流程请参考 [SKILL.md](SKILL.md)

---

## 📦 交付成果

完成 9 步流程后，你将获得：

| 类型 | 内容 | 说明 |
|------|------|------|
| 🎬 **视频文件** | `out/final-video.mp4` | 完整渲染视频（5-7 MB） |
| 📄 **内容文档** | `content/*.md` | 分析、结构、脚本、文案 |
| 🔊 **音频文件** | `public/audio/*.mp3` | 6个场景配音 |
| 🖼️ **视觉素材** | `output/*-card.png` | 项目信息卡封面图 |

---

## 🛠️ 技术栈

- **[Remotion](https://www.remotion.dev/)** - React 视频框架
- **[豆包 TTS](https://www.volcengine.com/product/166)** - 语音合成
- **[Gemini](https://ai.google.dev/)** - AI 深度分析
- **[Claude Code](https://claude.com/)** - 自动化工作流

---

## 🎬 视频示例

### 竖屏视频（1080×1920）
适用于：抖音、视频号、小红书

**典型结构（76秒）：**
- 场景1：开场钩子（10秒）- GitHub Star 数量滚动
- 场景2：痛点直击（10秒）- 传统方式的问题
- 场景3：方案登场（10秒）- 产品名称突出 ⭐
- 场景4：核心亮点（20秒）- 功能卡片展示
- 场景5：实际演示（18秒）- 使用流程
- 场景6：行动号召（8秒）- GitHub Star 引导

### 横屏视频（1920×1080）
适用于：B站、YouTube

**典型时长：** 90-120 秒

---

## 💡 最佳实践

### 时长控制
- 竖屏短视频：**60-90 秒**（推荐 76 秒）
- 横屏长视频：**90-120 秒**

### 场景3 产品名称突出
```tsx
// 超大字号渐变
background: "linear-gradient(135deg, #4ade80 0%, #22c55e 50%, #16a34a 100%)"
WebkitBackgroundClip: "text"
WebkitTextFillColor: "transparent"

// 脉冲动画
const logoPulse = Math.sin(frame * 0.1) * 0.05 + 1;

// 发光效果
filter: "blur(20px)"
```

### 音视频精确同步
- 每个场景帧数 = 音频时长(秒) × 30fps
- 场景起始帧 = 前面所有场景帧数之和
- Root.tsx 的 `durationInFrames` = 所有场景帧数总和

### Hook 开场（前3秒）
- ✅ 必须有数字（Star 数量、用户数）
- ✅ 必须有冲突感（痛点 vs 解决方案）
- ✅ 必须有代入感（场景化描述）

---

## 📚 相关资源

- [Remotion 官方文档](https://www.remotion.dev/)
- [Agent Skills 规范](https://agentskills.io/specification)
- [Claude Code 文档](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview)

---

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

---

## 📄 许可证

[MIT License](LICENSE) - 自由使用、修改、分发

---

## 👨‍💻 作者

**Abu + Claude**

- GitHub: [@cuishiqing](https://github.com/cuishiqing)
- Skill: [remotion-video-starter](https://github.com/cuishiqing/remotion-video-starter)

---

## 🌟 Star History

如果这个 skill 对你有帮助，请给个 Star ⭐️

---

<div align="center">

**[⬆ 回到顶部](#remotion-video-starter)**

Made with ❤️ by Abu + Claude

</div>

---

## English

A complete Remotion video production automation skill for creating product promotional videos.

**Features:**
- Auto-analyze GitHub projects and generate video concepts
- 9-step complete workflow from analysis to delivery
- Support both portrait (1080×1920) and landscape (1920×1080)
- Auto-generate voiceover, copy, and info cards
- Multi-platform support: TikTok, WeChat Video, Xiaohongshu, Bilibili, YouTube

**Installation:**
```bash
git clone https://github.com/cuishiqing/remotion-video-starter.git ~/.claude/skills/remotion-video-starter
```

**Usage:**
```
Use remotion-video-starter skill to create a promotional video for [project-name]
```

For detailed documentation, see [SKILL.md](SKILL.md)
