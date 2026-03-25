# UI Cloner

<p align="center">
  <strong>像素级 UI 设计系统提取工具</strong><br>
  <sub>Analyze UI screenshots → Extract complete design system → Generate reusable .skill file</sub>
</p>

---

## 概述

UI Cloner 是一个 Claude Code skill，能够分析任意产品的 UI 截图，提取完整的设计系统，并生成可复用的 `.skill` 文件。任何人都能够使用这个 skill 在任意技术栈中精确复刻相同的 UI。

### 核心特性

- **🎯 像素级精确提取** - 所有颜色值使用精确 HEX，尺寸精确到 px
- **📐 完整设计令牌** - 颜色、字体、间距、圆角、阴影
- **🧩 组件清单** - 所有组件的变体、状态、尺寸规格
- **📱 布局模式** - 页面模板、网格系统、导航结构
- **🎨 视觉风格** - 自动识别设计风格（Minimalism、Glassmorphism 等）
- **⚡ 交互模式** - 推断 hover/focus/loading 等状态行为

---

## 安装

### 方法一：项目本地安装（推荐）

```bash
cp ui-cloner.skill .claude/skills/
```

### 方法二：全局安装

```bash
cp ui-cloner.skill ~/.claude/skills/
```

---

## 使用方法

### 触发短语

- "Clone this UI" + 截图路径
- "Copy this design" + 图片目录
- "Extract the design system from these screenshots"
- "Reproduce this page"

### 示例

```
Clone this UI from my screenshots: ./designs/dashboard.png ./designs/settings.png
Product name: acme-app
```

### 生成的文件结构

```
{product-name}-ui/
├── SKILL.md              # 主 skill 文件
└── references/
    ├── design-tokens.md  # 颜色、字体、间距、圆角、阴影
    ├── components.md     # 组件清单及其变体和状态
    ├── layout.md         # 页面布局、网格系统、导航结构
    └── style-guide.md    # 视觉风格、交互模式、UX 原则
```

---

## 分析维度

每个截图都会进行 5 个维度的完整分析：

| 维度 | 提取内容 |
|------|----------|
| **设计令牌** | 完整调色板、字体尺度、间距网格、圆角、阴影 |
| **组件清单** | 所有 UI 组件及其变体、状态、尺寸、结构 |
| **布局结构** | 页面布局、网格系统、导航模式、响应式断点 |
| **视觉风格** | 风格分类（Glassmorphism/Minimalism 等）、图标风格、插画风格 |
| **交互模式** | 推断 hover/focus/loading 状态、动画风格、反馈模式 |

---

## 视觉验证（可选）

生成 skill 后，会询问：

> "是否需要生成示例页面并与原始截图进行视觉对比验证？"

如果同意，工具将：
1. 使用 `ui-ux-pro-max` 生成示例页面
2. 使用视觉 AI 对比生成页面与原始截图
3. 自动修正关键差异
4. 循环验证直到无关键差异

---

## 使用生成的 Skill

安装后，可在任何对话中使用：

```
"Use the acme-app-ui skill to build the login page in React + Tailwind"
"Add a settings page that matches the acme-app-ui design system"
"Build a dashboard using Next.js following the acme-app-ui style"
```

技术栈在调用时指定，skill 本身不绑定任何技术栈。

---

## 项目结构

```
copy-ui-skill/
├── README.md                    # 项目文档
├── SKILL.md                     # 主 skill 定义
├── ui-cloner.skill              # 打包的 skill 文件
├── references/
│   ├── analysis-guide.md        # 各维度提取指南
│   └── skill-template.md        # 生成的 skill 文件模板
├── .claude/skills/              # 示例生成的 skills
│   ├── demo-ui/                 # Demo App 示例
│   └── xshop-ui/                # XShop 示例
└── assets/                      # 截图和资源
```

---

## 示例

### demo-ui 示例

基于 `demo/1.jpeg` 提取的设计系统：

- **分析轮次**: 6 轮迭代像素级分析
- **主色调**: 4 个 + 功能色 8 个
- **字体尺度**: 6 级
- **间距基准**: 8px
- **核心组件**: 10 个
- **状态定义**: 完整 default/hover/active/disabled

查看: `.claude/skills/demo-ui/`

---

## 依赖

- Claude Code with `mcp__zai-mcp-server` MCP server（用于视觉分析和对比）
- `ui-ux-pro-max` skill（可选，用于代码生成和视觉验证）
- `skill-creator` skill（可选，用于打包）

---

## 许可证

MIT License

---

## 贡献

欢迎提交 Issue 和 Pull Request！

1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/amazing-feature`)
3. 提交更改 (`git commit -m 'feat: add amazing feature'`)
4. 推送到分支 (`git push origin feature/amazing-feature`)
5. 创建 Pull Request