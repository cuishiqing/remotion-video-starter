# Remotion Video Starter Skill

**版本：** v2.0
**最后更新：** 2026-03-24
**作者：** Abu + Claude

---

## Skill 概述

这是一个完整的 Remotion 视频制作自动化 skill，用于快速制作产品推广视频。

**核心能力：**
- 自动分析 GitHub 项目并生成视频创意
- 9步完整流程，从分析到交付
- 支持竖屏（1080×1920）和横屏（1920×1080）
- 自动生成配音、发布文案、信息卡

**适用场景：**
- GitHub 项目推广视频
- 开源项目介绍
- 产品功能演示

**输出格式：**
- 竖屏：抖音、视频号、小红书
- 横屏：B站、YouTube

---

## 使用方法

### 调用方式

```
使用 remotion-video-starter skill 为 [项目名称] 制作推广视频
```

### 必需输入

1. **GitHub URL** 或 **项目名称**
2. **视频格式**（可选，默认竖屏）
3. **目标时长**（可选，默认76秒）

---

## 9步完整流程

### 步骤 1：Gemini 深度分析项目

**目的：** 理解项目的核心价值、亮点、目标用户

**操作：**
```bash
调用 Gemini 分析项目
输入：GitHub URL
输出：content/01-主题分析.md
```

**输出内容包含：**
- 核心功能（3-5个）
- 目标用户（3-5类）
- 解决的痛点（3-5个）
- 独特优势（3-5个）
- 最吸引人的亮点（1-3个）
- 视频推广角度（标题建议、核心卖点、风格定位）
- 配色方案建议

---

### 步骤 2：设计视频结构

**目的：** 规划6场景结构和时间线

**操作：**
```bash
基于 01-主题分析.md 设计场景结构
输出：content/02-视频结构.md
```

**场景结构（76秒竖屏版）：**
- 场景1：开场钩子（10秒）- GitHub Star 数量滚动
- 场景2：痛点直击（10秒）- 传统方式的问题
- 场景3：方案登场（10秒）- 产品名称突出
- 场景4：核心亮点（20秒）- 功能卡片展示
- 场景5：实际演示（18秒）- 使用流程
- 场景6：行动号召（8秒）- GitHub Star 引导

**输出内容包含：**
- 每个场景的画面描述
- 配音方向
- 动画建议
- 时间线总览（帧数计算）
- 配色方案
- 动画库参考

---

### 步骤 3：编写配音脚本

**目的：** 创作6场景完整配音文案

**操作：**
```bash
基于 01 和 02 创作配音脚本
输出：content/03-配音脚本.md
```

**配音原则：**
- 场景1：有力、吸引注意（强调 Star 数量）
- 场景2：紧迫感、痛点共鸣
- 场景3：产品名称清晰有力（语速稍慢 1.1x）
- 场景4：平稳清晰、停顿强调
- 场景5：从容、步骤清晰
- 场景6：上扬、号召行动（语速稍快 1.15x）

**总字数控制：**
- 76秒视频：约 280-320 字
- 语速：约 2.2 字/秒（正常）到 2.8 字/秒（快）

---

### 步骤 4：复制模板项目并清理

**目的：** 快速搭建 Remotion 项目骨架

**操作：**
```bash
# 4.1 选择模板项目
cd ~/Documents/Claude\ Code/视频

# 竖屏视频（推荐）
cp -r social-analyzer-video [新项目名称]-video

# 横屏视频
# cp -r [横屏模板项目] [新项目名称]-video

# 4.2 进入新项目
cd [新项目名称]-video

# 4.3 清理旧文件
rm -rf public/audio/*.mp3
rm -rf out/*
rm -rf content/*.md
```

**模板项目位置：**
- 竖屏：`~/Documents/Claude Code/视频/social-analyzer-video/`（最新，9步流程）
- 横屏：`~/Documents/Claude Code/视频/[横屏模板]/`

---

### 步骤 5：更新 Remotion 配置

**目的：** 修改项目名称和配置

**操作：**
```bash
# 5.1 批量替换项目名称
cd src/compositions
# 使用 VSCode 或编辑器
# 查找：SocialAnalyzer
# 替换：[新项目名称，驼峰命名]

# 5.2 更新 Root.tsx
# 检查 durationInFrames 是否匹配步骤2的时间线
```

**关键配置：**
- `Root.tsx`：视频分辨率、总时长
- `remotion.config.ts`：项目配置
- `package.json`：项目名称

---

### 步骤 6：实现场景组件

**目的：** 根据步骤2的结构实现6个场景

**操作：**
```bash
# 基于 02-视频结构.md 修改每个场景组件
cd src/compositions

# 修改文件：
# - Scene1_Opening.tsx
# - Scene2_PainPoint.tsx
# - Scene3_Solution.tsx  ⭐ 最重要场景
# - Scene4_Features.tsx
# - Scene5_Demo.tsx
# - Scene6_CTA.tsx
```

**场景3特别说明（产品名称突出）：**
```tsx
// 1. 超大字号渐变
background: "linear-gradient(135deg, #4ade80 0%, #22c55e 50%, #16a34a 100%)"
WebkitBackgroundClip: "text"
WebkitTextFillColor: "transparent"

// 2. 脉冲动画
const logoPulse = Math.sin(frame * 0.1) * 0.05 + 1;

// 3. 发光效果
<div style={{
  background: `radial-gradient(circle, rgba(34, 197, 94, ${glowIntensity * 0.5}) 0%, transparent 70%)`,
  filter: "blur(20px)",
}} />

// 4. 扫描线动画
<div style={{
  top: `${(frame / 150) * 100}%`,
  height: "2px",
  background: "#00ff41",
}} />
```

---

### 步骤 6.4：添加固定尾帧

**目的：** 统一品牌识别，提升效率

**操作：**
```bash
# 6.4.1 创建 Scene7_Ending.tsx 组件
# 基于模板项目的 Scene7_Ending.tsx

# 6.4.2 复制尾帧文件
cp ~/Documents/Claude\ Code/视频/assets/ending-frames/default.mp4 \
   public/scenes/scene7-ending.mp4

# 6.4.3 添加到主组件时间线
# 在 [ProjectName]Video.tsx 中：
<Sequence from={2280} durationInFrames={148}>
  <Scene7_Ending />
</Sequence>

# 6.4.4 更新 Root.tsx 总时长
durationInFrames={2428}  # 2280 + 148
```

**尾帧映射表：**
| 视频类型 | 推荐尾帧 | 文件名 |
|---------|---------|--------|
| 通用产品 | 主账号宣传 | default.mp4 |
| 科技/创新 | （未来）科技风格 | alternative-tech.mp4 |
| B端/专业 | （未来）极简风格 | alternative-minimal.mp4 |

**默认使用：** `default.mp4`（主账号宣传，4.93秒，148帧）

---

### 步骤 7：生成配音音频

**目的：** 使用豆包TTS生成6个场景配音

**操作：**
```bash
# 7.1 创建音频生成脚本
cd scripts
cp ~/Documents/Claude\ Code/视频/social-analyzer-video/scripts/generate_audio.py .

# 7.2 修改脚本中的文案
# 编辑 generate_audio.py
# 替换 SCENES 数组中的文案为步骤3的内容

# 7.3 生成音频
python3 generate_audio.py
```

**豆包TTS配置：**
```python
VOLC_API_KEY = "你的豆包API Key"
VOLC_TTS_URL = "https://openspeech.bytedance.com/api/v1/tts"
VOICE_TYPE = "zh_male_liufei_uranus_bigtts"  # 刘飞声音
CLUSTER_ID = "volcano_tts"
```

> 💡 **获取 API Key：** 访问 [火山引擎](https://console.volcengine.com/speech/service)

**预期输出：**
```
public/audio/
├── scene1.mp3
├── scene2.mp3
├── scene3.mp3
├── scene4.mp3
├── scene5.mp3
└── scene6.mp3
```

---

### 步骤 8：生成视频号发布文案

**目的：** 生成适配视频号的发布文案

**操作：**
```bash
基于 01-主题分析.md 和 03-配音脚本.md
输出：content/08-发布文案.md
```

**内容结构：**
1. **短标题**（16字符以内）
2. **开头钩子**（来自配音脚本场景1）
3. **核心亮点**（3-5个，来自主题分析）
4. **价值升华**（一句话总结）
5. **行动号召**（来自配音脚本场景6）
6. **热门标签**（3-5个相关标签）

**示例：**
```
【标题】22,000+ Star！全网账号一键扫描 🔍

【开头】
你的网络"分身"藏不住了！
1分钟找到你在1000个网站的踪迹

【核心亮点】
✅ 支持 1000+ 社交媒体和网站
✅ 智能评分系统，精准定位
✅ 多层次检测 + OCR 光学字符识别
✅ 可视化图谱分析

【价值升华】
安全专家和执法机构都在用的 OSINT 神器

【行动号召】
开源免费，链接在评论区！快去试试看吧！

【标签】
#网络安全 #OSINT #开源工具 #GitHub推荐
```

---

### 步骤 9：生成信息卡

**目的：** 生成项目信息卡图片，用于视频封面

**操作：**
```bash
调用 Gemini 生成 HTML 信息卡
输出：output/[项目名称]-card.html
```

**核心原则：**
1. 信息卡目标是让用户**通过图片理解产品价值**
2. 内容必须丰富、具体、有说服力
3. 必须从多个文档汇总，不能简单列举
4. 列出具体名称（播客名、人名），不只是数字

**内容结构（7个部分）：**
1. **痛点引入** - 场景化描述，引起共鸣
2. **核心理念** - 产品 Slogan
3. **具体数据** - 列出播客名、人名（不只是数字）
4. **核心功能** - 详细说明（不只简单列举）
5. **使用方法** - 操作步骤、所需时间
6. **目标用户** - 适合人群
7. **行动号召** - GitHub、Star

**样式选择：**
从以下2个样式中选择：
1. **终端风格**（科技产品）
2. **卡片风格**（通用产品）

**错误示例 vs 正确示例：**

❌ **错误：**
```
核心亮点：
- 支持1000+网站
- 智能评分系统
- 可视化图谱
```

✅ **正确：**
```
核心亮点：
- 1000+ 网站：Facebook、Twitter、Instagram、抖音、微博、B站等主流平台
- 智能评分：0-100 分可信度评分，有效降低假阳性
- 可视化图谱：力导向图展示账号关联，元数据提取
```

**生成预览：**
```bash
# 使用 HTML 预览工具
# 或直接在浏览器中打开 HTML 文件
```

**转图片：**
```bash
# 使用截图工具或命令行工具
# 推荐尺寸：600×900px（竖屏封面）
```

---

## 步骤 10：调试和渲染

### 步骤 10.1：启动开发服务器

```bash
cd ~/Documents/Claude\ Code/视频/[新项目名称]-video
npm start
```

访问：http://localhost:3000

### 步骤 10.2：检查清单

**内容检查：**
- [ ] 所有6个场景的文案正确
- [ ] 文字清晰可读
- [ ] 颜色对比度足够
- [ ] 无错别字

**动画检查：**
- [ ] 动画流畅不卡顿
- [ ] 过渡自然
- [ ] 重点信息有动画强调

**音频检查：**
- [ ] 音频播放正常
- [ ] 音量适中（建议 0.9）
- [ ] 音频与画面同步
- [ ] 无静音等待

### 步骤 10.3：渲染最终视频

```bash
# 渲染完整视频
npx remotion render src/index.jsx [ProjectName]Video out/final-video.mp4 \
  --codec=h264 --pixel-format=yuv420p --overwrite

# 渲染单个场景（用于测试）
npx remotion render src/index.jsx [ProjectName]Video out/scene1.mp4 \
  --sequence --frames=0-299
```

**预期输出：**
```
✓ out/final-video.mp4 (约 5-7 MB)
```

---

## 交付成果清单

完成9步流程后，你应该得到：

### 1. 视频文件
- [ ] `out/final-video.mp4` - 完整视频
- [ ] `out/scene1.mp4` 到 `out/scene6.mp4` - 分场景视频（可选）

### 2. 内容文档
- [ ] `content/01-主题分析.md` - Gemini 深度分析
- [ ] `content/02-视频结构.md` - 6场景结构设计
- [ ] `content/03-配音脚本.md` - 完整配音文案
- [ ] `content/08-发布文案.md` - 视频号发布文案
- [ ] `content/04-完成报告.md` - 项目总结

### 3. 音频文件
- [ ] `public/audio/scene1.mp3` 到 `scene6.mp3` - 6个场景配音

### 4. 视觉素材
- [ ] `output/[项目名称]-card.png` - 项目信息卡封面图

---

## 参考资源

### 模板项目
- 竖屏：`~/Documents/Claude Code/视频/social-analyzer-video/`
- 横屏：`~/Documents/Claude Code/视频/[横屏模板]/`

### 工作文档
- `~/Documents/Claude Code/视频/工作流/Remotion视频制作标准化工作流.md`
- `~/Documents/Claude Code/视频/工作流/视频项目模板.md`
- `~/Documents/Claude Code/视频/工作流/templates/README.md`

### 尾帧管理
- `~/Documents/Claude Code/视频/assets/ending-frames/`
- `~/Documents/Claude Code/视频/assets/ending-frames/README.md`

---

## 最佳实践

### 1. 时长控制
- 竖屏短视频：60-90秒（推荐76秒）
- 横屏长视频：90-120秒

### 2. 场景3突出产品名称
- 超大字号渐变
- 脉冲动画
- 发光效果
- 扫描线动画
- 配音语速稍慢（1.1x）

### 3. 音视频精确同步
- 每个场景帧数 = 音频时长(秒) × 30fps
- 场景起始帧 = 前面所有场景帧数之和
- Root.tsx 的 `durationInFrames` = 所有场景帧数总和

### 4. 配色方案
根据项目类型选择：
- 科技产品：黑客绿 + 深黑
- B端产品：科技蓝 + 深灰
- 消费产品：渐变色 + 浅色

### 5. Hook 开场（前3秒）
- 必须有数字（Star 数量、用户数）
- 必须有冲突感（痛点 vs 解决方案）
- 必须有代入感（场景化描述）

---

## 常见问题

### Q1: 如何选择模板项目？
竖屏视频使用 `social-analyzer-video`，横屏视频使用其他横屏模板项目。

### Q2: 音频生成失败怎么办？
确认豆包TTS API Key配置正确，检查网络连接，不要擅自改用其他TTS服务。

### Q3: 渲染时提示 "No entry point specified"？
```bash
# 必须指定入口点
npx remotion render src/index.jsx [ProjectName]Video out/video.mp4
```

### Q4: 音频在场景结尾被截断？
检查音频实际时长，增加 `durationInFrames`，调整后续场景的 `from` 参数。

### Q5: 信息卡内容不够丰富？
必须从多个文档汇总（01、02、03），列出具体名称，不只是数字。

---

## 更新日志

**v2.0 (2026-03-24)：**
- 新增步骤8：视频号发布文案生成
- 新增步骤9：信息卡生成
- 步骤6.4：添加固定尾帧自动化
- 更新为9步完整流程

**v1.0 (2026-03-13)：**
- 初始版本，7步流程

---

**Skill 维护者：** Abu + Claude
**最后验证项目：** Social Analyzer 视频（2026-03-24）
**使用次数：** 20+ 项目
**平均耗时：** 首次 4-6 小时，复用 2-3 小时
