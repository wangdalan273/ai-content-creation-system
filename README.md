# AI Content Creation System

用 Obsidian + Claude Code 搭建一套 AI 内容创作系统，从零散想法到公众号草稿箱，三步走完一条内容。

## 这是什么

一套完整的 AI 辅助内容创作工作流，包含：

- **wechat-writing Skill** -- Claude Code 的写作技能，支持三种文章风格（技术博客 / 评测对比 / 观点洞察），自动匹配风格、补充最新信息、优化标题和结构
- **三个模板文件** -- 品牌定位、创作流程、目录结构，填完就能用
- **排版插件指引** -- 推荐使用 obsidian-wechat-converter 插件，在 Obsidian 里排版并一键同步到公众号草稿箱

## 工作流程

```
灵感捕捉 → 素材积累 → 对话打磨 → Skill创作 → 排版发布
```

1. **对话打磨** -- 在 Obsidian 里打开 Claude Code，把想法、素材、语音笔记丢进去和 AI 聊，聊出框架
2. **Skill 创作** -- 调用 wechat-writing Skill，AI 按你设定好的规则生成文章、备选标题、配图建议
3. **排版发布** -- 用排版插件一键同步到公众号草稿箱，检查后发布

整个过程在 Obsidian 里完成，不用切换工具。

## 快速开始

### 前置要求

- [Obsidian](https://obsidian.md) 已安装
- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) 已安装并能正常运行
- 公众号账号（需要 AppID 和 AppSecret 用于插件同步）

### 第一步：安装 Skill

1. 找到你的 Claude Code skill 安装目录（通常在 `~/.agents/skills/` 或 `~/.claude/skills/`）
2. 将本仓库的 `skill/` 文件夹整体复制进去，重命名为 `wechat-writing`
3. 目录结构应该是：

```text
wechat-writing/
├─ SKILL.md                    ← 主文件，Claude Code 会读取这个
├─ references/
│  ├─ writing-style.md         ← 写作风格规范
│  ├─ books.md                 ← 引用书籍和金句库
│  ├─ title-formulas.md        ← 32个标题公式
│  ├─ quality-checklist.md     ← 质量自检清单
│  ├─ image-guide.md           ← 配图指南
│  └─ writing-techniques.md    ← 通用写作技巧
└─ assets/
   ├─ template-structure.md    ← 文章结构模板
   ├─ emoji-library.txt        ← Emoji 素材库
   └─ 配图风格/                ← 配图风格提示词模板
```

### 第二步：配置个人信息

1. 复制 `templates/品牌定位模板.md` 到你的 Obsidian Vault
2. 填写你的账号名、读者画像、内容方向、语气风格
3. 复制 `templates/内容创作系统说明模板.md` 到你的 Vault
4. 根据需要调整创作流程和规则

### 第三步：配置 Skill 路径

打开 `skill/SKILL.md`，找到路径配置部分，替换占位符：

```text
{vault根目录}  →  你的 Obsidian Vault 的实际路径
{你的skill安装目录}  →  你安装 skill 的实际路径
{你的系列名}  →  你的系列名（如果不用系列，删掉相关段落）
{你的账号名}  →  你的公众号名称
```

### 第四步：安装排版插件

本仓库已包含 obsidian-wechat-converter 插件的分发文件（`plugin/` 目录）。

1. 将 `plugin/` 文件夹整体复制到你的 Obsidian Vault 的 `.obsidian/plugins/wechat-converter/` 目录下
2. 在 Obsidian 设置 → 社区插件 中启用 "Wechat Converter"
3. 在插件设置中填入你的公众号 AppID 和 AppSecret（在公众号后台 → 开发 → 基本配置中获取）
4. 原项目地址：[obsidian-wechat-converter](https://github.com/DavidLam-oss/obsidian-wechat-converter)

### 第五步：跑通一次

1. 在 Obsidian 里打开 Claude Code
2. 给 AI 一个选题，说"帮我写一篇关于 XX 的文章"
3. AI 会走完从素材分析到文章生成的流程
4. 用排版插件同步到公众号草稿箱
5. 检查后发布

## Vault 目录结构建议

详见 `templates/Vault目录结构.md`，核心结构：

```text
你的Vault/
├─ 01_内容创作/
│  ├─ 00_内容创作规范/     ← 系统规则文件
│  ├─ 01_选题池/           ← 灵感记录
│  ├─ 02_内容生产中/       ← 正在写的文章
│  └─ 03_已发布内容/       ← 写完按月归档
├─ 02_资料库/
├─ 03_日记复盘/
└─ 04_学习输入/
```

每篇文章独立目录：

```text
01_内容创作/02_内容生产中/YYYYMMDD-标题/
├─ 00_内容卡片.md          ← 元数据（title + description + 状态）
├─ 01_文章内容/
│  ├─ 公众号文章.md         ← 正文（frontmatter 含 title 和 description）
│  ├─ 配图建议.md
│  └─ images/
├─ 02_视频素材/
├─ 03_封面图/
├─ 04_最终视频/
└─ 05_发布文案/
    └─ 跨平台发布文案.md    ← 抖音/B站/小红书文案
```

## 三种文章风格

| 风格 | 触发词 | 适用场景 |
|------|--------|---------|
| 技术博客（B） | 教程、实操、工具、踩坑 | 工具使用心得、教程、效率提升 |
| 评测对比（D） | 评测、对比、选哪个、A vs B | 工具横评、方案选择 |
| 观点洞察（E） | 观点、趋势、为什么、思考 | 行业分析、趋势判断、个人方法论 |

## 文章 Frontmatter 规则

公众号文章需要有 frontmatter，供排版插件读取标题和摘要：

```yaml
---
title: 文章标题
description: 公众号摘要，100字以内
---
```

对应的内容卡片（00_内容卡片.md）也需要包含这两个字段，Skill 会自动同步。

## 自定义进阶

- **风格样本** -- 把你写过的满意文章放进 Vault，在品牌定位文件中引用，AI 会学习你的表达方式
- **标题公式** -- `references/title-formulas.md` 包含 32 个标题公式，可以根据你的风格增删
- **配图风格** -- `assets/配图风格/` 下有多个风格模板，可以修改配色适配你的品牌
- **质量自检** -- `references/quality-checklist.md` 可以加入你自己的检查项

## 许可

- 本仓库的 Skill 和模板文件基于 MIT 许可
- obsidian-wechat-converter 插件遵循其自身的开源许可，详见 [插件仓库](https://github.com/DavidLam-oss/obsidian-wechat-converter)
