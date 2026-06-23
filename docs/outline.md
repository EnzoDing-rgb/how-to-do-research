# How to do Research · 科研方法分享

> **核心主张**：AI 时代做科研，卡在两处——**个人上下文的上限**（想多深、读多广）和**执行的效率**（想法能否落地）。  
> 今天分享两条互补路径：**OpenCode** 拉高执行力，**Vibero** 扩展阅读上下文；不是推销，是科研方法论。  
> **封面主标题**：`How to do Research` · 副标题：`科研方法分享`  
> **页数**：7 页  
> **禁止出现**：Zotero · Research Assistant · Claude Code

---

## 生产架构（以终为始）

最终交付 = **花叔 design HTML deck**（浏览器翻页）+ **Ian Handdrawn 文生图**（装饰性手绘区）+ **真实产品截图嵌入**。

```
docs/outline.md          ← 本文件（内容 + 每页 handler 规格）
        ↓
deck/                    ← 花叔 design 产出（待生成）
├── index.html           ← 翻页聚合（仿 research-assistant/deck/index.html）
├── start.sh
├── shared/
│   ├── handdrawn.css    ← Ian visual DNA tokens（#FBFAF5 纸底等）
│   ├── fonts.css
│   └── nav-keys.js
├── slides/
│   ├── 01-cover.html
│   └── … 07-closing.html
└── assets/
    ├── screenshots/     ← 从 ../assets/ 复制或引用
    │   ├── opencode-home.png
    │   ├── vibero-brand.png
    │   └── vibero-nonlinear.png
    └── generated/         ← Ian 文生图 PNG（placeholder → 最终图）
        ├── slide-02-philosophy.png
        ├── slide-04-demo-frame.png
        └── …
```

### 双 Skill 分工

| Skill | 路径 | 负责什么 |
|-------|------|----------|
| **花叔 design** | `.agents/skills/huashu-design/`（本 repo 已装） | HTML 幻灯片骨架、翻页、手绘 CSS grammar、截图窗框（`macos_window` / `browser_window`）、fancy 视觉层 |
| **Ian Handdrawn PPT** | `~/.agents/skills/ian-handdrawn-ppt/`（全局；生成 deck 前可 `cp -R` 到本 repo `.agents/skills/`） | 中央语义区 **整页或半页 PNG**；文生图 prompt 按 Visual DNA V6 |

### 视觉合成策略（手绘 + 截图不矛盾）

每页 = **固定 Ian 外壳**（纸底、页码、标题、淡蓝下划线、角标网格）+ **可变中区**：

| 页类型 | 中区内容 | 做法 |
|--------|----------|------|
| 概念/哲学页 | 纯手绘隐喻图 | Ian 文生图 → `deck/assets/generated/` → HTML `<img>` 嵌入 |
| 产品介绍页 | 截图为主 | 花叔 `browser_window` 框嵌入 `screenshots/*.png`；手绘角标/箭头叠在截图外 |
| Demo 页 | 截图 + 手绘动线 | 大图截图居中；手绘编号圆圈 ①②③ 用 CSS/SVG；可选 Ian 生成「Live Demo」角标插画 |
| 封面 | 21:9 隐喻（可选）或 16:9 | Ian 生成封面隐喻；HTML 叠双语标题 |

### Deck Style Lock（Ian · 全页复用）

```text
Refined commercial Chinese handdrawn technical PPT illustration.
Complete raster on very light warm white paper #FBFAF5, extremely subtle grain.
No full-page border. Upper-left page number "NN / 07".
Centered medium Chinese title, one pale blue handdrawn underline.
Fine black ink + pencil hatching. Pastel labels: #D9E8F6 #DCEAD6 #F5DEB8 #E4DCF4.
Sparse corner grid/dot construction marks. Large negative space.
At most one tiny reader character in corner. No yellow paper, no gradients, no AI slop purple.
```

### 花叔 CSS Tokens（HTML 层 · 与 Ian 对齐）

```css
--paper: #fbfaf5;  --ink: #1a1a1a;  --muted: #5f5a50;
--blue: #d9e8f6;   --green: #dcead6; --peach: #f5deb8; --lavender: #e4dcf4;
--font-hand: "Patrick Hand", "Ma Shan Zheng", "Noto Sans SC", cursive;
```

参考实现：`../research-assistant/deck/shared/handdrawn.css`

### 文生图 Placeholder 约定

生成 deck 前，HTML 里先用灰色块：

```html
<!-- PLACEHOLDER: slide-02-philosophy.png · see outline §第2页 Image Prompt -->
<div class="img-placeholder" data-prompt-id="slide-02">手绘区待生成</div>
```

Prompt 全文写在本 outline 对应页；生成后替换为 `<img src="../assets/generated/slide-02-philosophy.png">`。

**推荐模型**：ChatGPT Image 2.0（Ian 默认）；Cursor `GenerateImage` 可作试探，中文不稳时减字或后处理叠字。

### 截图资产映射

| 源文件 | 复制为 | 用于 |
|--------|--------|------|
| `assets/Screenshot 2026-06-17 at 22.19.27.png` | `deck/assets/screenshots/opencode-home.png` | 第 3、4 页 |
| `assets/Screenshot 2026-06-17 at 22.17.15.png` | `deck/assets/screenshots/vibero-brand.png` | 第 5 页 |
| `assets/Screenshot 2026-06-17 at 22.18.27.png` | `deck/assets/screenshots/vibero-nonlinear.png` | 第 6 页 |

---

## 叙事弧线

```
01 封面：How to do Research
    ↓
02 哲学：上下文上限 × 执行效率（非线性注意力预告）
    ↓
03 OpenCode 是什么
    ↓
04 OpenCode Live Demo（页内占位；现场浏览器演示）
    ↓
05 Vibero 是什么（一页浓缩）
    ↓
06 Vibero Live Demo（Transformer 示例）
    ↓
07 收束：两条腿 · 方法论不是推销
```

---

## 第 1 页 · 封面

| 项 | 内容 |
|----|------|
| **Archetype** | Cover metaphor |
| **Canvas** | 16:9（1920×1080）；封面隐喻区可按 Ian 规范另出 21:9 备用 |
| **页码** | `01 / 07` |

### 页上文字（HTML 精确渲染 · 不依赖生图）

```
How to do Research
科研方法分享
扩展上下文 · 提升执行力
```

角标小字（可选）：`OpenCode` · `Vibero`

### HTML Handler（`slides/01-cover.html`）

- `handdrawn.css` 全页纸底 + 角标网格
- 居中 `h1` 英文主标题 + `p.subtitle` 中文
- 中央区：**二选一**  
  - A）Ian 生成的封面隐喻 PNG 作背景插图（opacity 0.9）  
  - B）纯 CSS 手绘双轴简图（纵轴「上下文」横轴「执行力」）作 fallback
- 底部 `tag-row`：两个手绘标签 `OpenCode` `Vibero`

### Image Prompt · `slide-01-cover.png`（可选，21:9 或 16:9）

```text
Page role: cover image. Canvas 16:9, 1920x1080.
Archetype: cover metaphor.
Main point: Research needs both wider context and faster execution.

Apply deck style lock: [paste Deck Style Lock above].

Composition: Small refined handdrawn diagram at center—two perpendicular axes forming a quiet cross. Vertical axis labeled with tiny pastel tag "上下文". Horizontal axis labeled "执行力". At the intersection, a tiny open notebook and a small terminal window sketched in fine ink. Large negative space around the diagram. No characters.

Required text only:
标题：科研方法分享
副标题：扩展上下文 · 提升执行力
```

### Speaker Notes

- 今天不是产品推销，是 **怎么做研究** 的方法分享。
- 科研常卡两处：想得不宽、做得太慢；后面两个工具分别对应两条腿。

---

## 第 2 页 · 哲学：两条瓶颈 ★

| 项 | 内容 |
|----|------|
| **Archetype** | Left-right contrast + main metaphor |
| **页码** | `02 / 07` |

### 页上文字

```
科研的两条腿
上下文上限 × 执行效率

想法重要 · 工具执行 · 阅读扩展边界
非线性分配注意力
```

### 三区内容（页上短句）

1. **左 · 上下文上限** — 经典文献 + 前沿论文飞入小书架；个人边界有限。  
2. **右 · 执行效率** — 终端/齿轮 → 清洗、整理、复现、写作。  
3. **底 · 桥** — 真正读文献不是线性扫 PDF；是 **跳读、对照、追问**（非线性注意力）。

### HTML Handler（`slides/02-philosophy.html`）

- 上半：标题区（HTML 文字）
- 下半：**Ian PNG 占宽 55%** 居中，或左右两栏 HTML + 中央手绘插图
- 不用截图

### Image Prompt · `slide-02-philosophy.png` ★ 建议文生图

```text
Page role: body illustration. Canvas 16:9, 1920x1080.
Page number exactly: 02 / 07
Title exactly: 科研的两条腿
Subtitle exactly: 上下文上限 × 执行效率
Archetype: left-right contrast.
Main point: Research is limited by personal context and execution speed.

Apply deck style lock + reference match clause.

Composition: Left group—small handdrawn bookshelf with a few floating paper sheets labeled with tiny pastel tags "经典" and "前沿", a small head silhouette above suggesting limited personal boundary. Right group—small terminal window and gear with arrow to tiny tags "整理" "复现". Thin dashed bridge at bottom connecting both sides with label "非线性注意力". Central diagram 55% page width. No more than one tiny reader in lower corner.

Required text only:
页码：02 / 07
标题：科研的两条腿
副标题：上下文上限 × 执行效率
左标：上下文
右标：执行力
底注：非线性注意力
```

### Speaker Notes

- 整堂课的「魂」：后面 OpenCode / Vibero 都落在这两条腿上。
- **非线性注意力**：人读 paper 本就跳读；关键是把注意力花在刀刃上。

---

## 第 3 页 · OpenCode 是什么

| 项 | 内容 |
|----|------|
| **Archetype** | Single concept explainer + product frame |
| **页码** | `03 / 07` |

### 页上文字

```
OpenCode
开源 AI 编程 Agent

终端 · 桌面 · IDE
连接多种模型 · 读懂项目上下文
```

### 要点（旁注或 HTML 侧栏，极简）

| 维度 | 一句话 |
|------|--------|
| 是什么 | 开源 Agent：读代码库、改文件、多步执行任务 |
| 模型 | 内置免费模型；可接 GPT / Gemini 等 |
| 对科研 | 问卷清洗、脚本、批处理、报告骨架——**想法 → 可运行产物** |
| vs 聊天 | 有项目上下文、Todo 拆解、多步执行（见截图右侧） |

### HTML Handler（`slides/03-opencode-intro.html`）

- 左 40%：标题 + 四条要点（`handdrawn` 列表样式）
- 右 55%：**花叔 browser_window** 嵌入 `screenshots/opencode-home.png`
  - 窗框手绘描边（`box-shadow` sketch 风格）
  - 截图内已有中文「开源 AI 编程代理」— 不重复造字
- 右栏外：三个手绘小图标标注「终端」「桌面」「IDE」

### Image Prompt

**本页可不生成整页 PNG**（截图为主）。可选生成 `slide-03-icons.png`：三个 tiny terminal/monitor/IDE sketches for sidebar—仅当 CSS 手绘图标不够时。

### Speaker Notes

- 强调 **执行力**：不是教编程，是用 Agent 做研究工序。
- 截图指给学生看 Context / Todo 面板。

---

## 第 4 页 · OpenCode Live Demo ★

| 项 | 内容 |
|----|------|
| **Archetype** | Horizontal process + demo stage |
| **页码** | `04 / 07` |
| **现场** | **你在浏览器现场演示安装**；本页只做视觉占位，不写复杂安装脚本 |

### 页上文字

```
OpenCode · Live Demo

现场安装 · 现场演示
```

### HTML Handler（`slides/04-opencode-demo.html`）— fancy 视觉层

- 全页 **舞台感**布局（花叔：深色渐隐条 + 纸底舞台，避免紫渐变 AI slop）
- 中央大区域：`LIVE` 手绘徽章 + 虚线框 **「演示区」**（空框，投影时切到浏览器）
- 左侧竖条：三步手绘编号（仅视觉，不绑死流程）  
  `① 打开 opencode.ai` → `② 安装客户端` → `③ 跑一个任务`
- 右下角：小窗 `screenshots/opencode-home.png` 作 teaser（opacity 0.85，手绘箭头指向 LIVE 区）
- 可选 CSS 微动效：`LIVE` 点缓慢 pulse（`@keyframes`，纯 CSS）

### Image Prompt · `slide-04-demo-badge.png`（可选装饰）

```text
Page role: body illustration. 16:9 but only generate a small corner badge asset on transparent or paper background.
Small handdrawn "LIVE" ribbon flag in fine ink, pale red-orange accent dot, sage green pastel fill. No other text. For overlay on HTML slide.
```

### Speaker Notes

- 页内文字刻意少；**安装与 Demo 全在浏览器完成**。
- 指一下 Context 用量：人在把关，Agent 在执行。
- 收束一句：执行力这条腿；下一部分讲上下文。

---

## 第 5 页 · Vibero 是什么（一页浓缩）

| 项 | 内容 |
|----|------|
| **Archetype** | Classification map + product frame |
| **页码** | `05 / 07` |

### 页上文字

```
Vibero · 氛围阅读
Meet the AI for vibe reading

更快，也更深 — 重新分配注意力
```

### 能力（页上四词，一行一个）

| 能力 | 一句话 |
|------|--------|
| **非线性阅读** | 静态 PDF → 交互式 AI 画布 |
| **核心点定位** | 先抓结构/论点，再决定细读哪里 |
| **画布 ↔ 对话** | 点选进上下文；问答拖回画布当笔记 |
| **论文 + 代码** | 同一工作区理解方法与实现 |

### HTML Handler（`slides/05-vibero-intro.html`）

- 上：标题 + 英文 tagline（与截图一致）
- 中：**browser_window** 嵌入 `screenshots/vibero-brand.png`（vibero.dev 品牌页）
- 下：四枚手绘 pastel 标签横排（非线性阅读 / 核心点定位 / 画布对话 / 论文代码）
- **禁止**出现任何文献管理工具名称

### Image Prompt

本页以截图为主，可不整页生图。可选 Ian 生成 `slide-05-four-tags.png`：四个 pastel 标签手绘排列，文字与上表一致（中文各 4–6 字）。

### Speaker Notes

- **Vibe Reading** = 按研究节奏分配注意力，不是替代精读。
- 产品哲学 = **非线性注意力** 的工具化（下页 Demo）。

---

## 第 6 页 · Vibero Live Demo ★

| 项 | 内容 |
|----|------|
| **Archetype** | Horizontal process + screenshot |
| **页码** | `06 / 07` |
| **示例论文** | **Attention Is All You Need（Transformer）** — 暂用截图，现场可同流程 |

### 页上文字

```
Live Demo · 非线性阅读
先见森林，再见树木

示例：Transformer 论文
```

### Demo 动线（页上手绘编号 · Speaker Notes 展开）

```
① 打开论文 → ② VIBE 解析出结构树 → ③ 点选段落追问 → ④ 笔记留在画布
```

### HTML Handler（`slides/06-vibero-demo.html`）

- 主图：`screenshots/vibero-nonlinear.png` 全宽 85%，**macos_window** 框
- 左侧叠手绘编号 ①–④ + 细箭头指向截图对应区域（结构树 / 高亮句 / 翻译气泡）
- 底部窄条：`示例：Attention Is All You Need`

### Image Prompt · `slide-06-flow-arrows.png`（可选）

仅生成手绘箭头/编号装饰条 PNG 用于叠在截图左侧；**不要**重新生成整张产品 UI（已有截图）。

```text
Small vertical strip asset: handdrawn circled numbers 1 2 3 4 with thin arrows pointing right, fine ink on near-white paper, no other text. For slide overlay.
```

### Speaker Notes

- Demo 重点：**阅读节奏变了**— 先结构、后细节、随时追问。
- Transformer 只是示例；流程适用于任何方法论文。
- 对照第 2 页：这是在扩展 **上下文上限**。

---

## 第 7 页 · 收束

| 项 | 内容 |
|----|------|
| **Archetype** | Takeaway |
| **页码** | `07 / 07` |

### 页上文字

```
方法论，不是推销

读得更宽 · 做得更快
想法在你 · 工序可自动化

Q & A
```

### HTML Handler（`slides/07-closing.html`）

- 中央：Ian PNG 或 CSS 双格对比  
  - 左格 `Vibero` + 小书架图标 → 「上下文」  
  - 右格 `OpenCode` + 小终端 → 「执行力」  
  - 底部汇合箭头 → 「更好的问题 + 更快的验证」
- 底：`Q & A` 手绘字

### Image Prompt · `slide-07-closing.png` ★ 建议文生图

```text
Page role: body illustration. 16:9, 1920x1080.
Page number exactly: 07 / 07
Title exactly: 方法论，不是推销
Subtitle exactly: 读得更宽 · 做得更快
Archetype: takeaway.
Main point: Two tools, one philosophy—expand context and execution.

Apply deck style lock.

Composition: Two small handdrawn panels side by side. Left panel: tiny book stack and canvas sketch, pastel blue label "上下文". Right panel: tiny terminal, pastel peach label "执行力". Both panels connect with quiet arrows to a small center note "研究". Bottom center small text area for Q&A. Large negative space. No product logos.

Required text only:
页码：07 / 07
标题：方法论，不是推销
副标题：读得更宽 · 做得更快
左标：上下文
右标：执行力
底字：Q & A
```

### Speaker Notes

- 三句收束：  
  1. AI 时代科研 = **扩展上下文 + 提升执行**。  
  2. **判断在人**；工具负责读与跑。  
  3. **非线性注意力** 是阅读观；**Agent 执行** 是落地观——工具可换，哲学不变。  
- Q&A：安装、API Key、AI 辅助写作边界等。

---

## `index.html` Manifest（生成 deck 时用）

```javascript
window.DECK_MANIFEST = [
  { file: "slides/01-cover.html",       label: "封面" },
  { file: "slides/02-philosophy.html", label: "两条瓶颈 ★" },
  { file: "slides/03-opencode-intro.html", label: "OpenCode" },
  { file: "slides/04-opencode-demo.html",  label: "OpenCode Demo ★" },
  { file: "slides/05-vibero-intro.html",   label: "Vibero" },
  { file: "slides/06-vibero-demo.html",    label: "Vibero Demo ★" },
  { file: "slides/07-closing.html",      label: "收束" },
];
window.DECK_WIDTH = 1920;
window.DECK_HEIGHT = 1080;
```

---

## 文生图产出清单

| 文件 | 优先级 | 用于页 |
|------|--------|--------|
| `slide-02-philosophy.png` | **高** | 第 2 页中央插图 |
| `slide-07-closing.png` | **高** | 第 7 页中央插图 |
| `slide-01-cover.png` | 中 | 第 1 页背景隐喻（可用 CSS fallback） |
| `slide-04-demo-badge.png` | 低 | LIVE 角标装饰 |
| `slide-06-flow-arrows.png` | 低 | 第 6 页箭头叠层 |

第 3、5 页以 **截图 + 花叔 HTML 手绘框** 为主，不强制整页生图。

---

## 生成 deck 前检查清单

- [ ] 复制三张截图 → `deck/assets/screenshots/`
- [ ] 生成高优先级 Ian PNG → `deck/assets/generated/`
- [ ] 先做 **01 封面 + 02 哲学** 两页 showcase（花叔规范：≥5 页 deck 先定 grammar）
- [ ] 确认全文无 Zotero / Research Assistant / Claude Code
- [ ] `index.html` + `start.sh` 可本地翻页
- [ ] （可选）`ian-handdrawn-ppt` 复制到本 repo `.agents/skills/` 方便 Cursor 读 reference

---

## 下一步（你确认后再做）

1. 你确认本 outline 内容无误  
2. 生成 `deck/` HTML（花叔 design 工作流）  
3. 按上表跑文生图填 placeholder  
4. `./deck/start.sh` 浏览器预览
