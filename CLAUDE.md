# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

这是一个**个人知识库**，用于积累和沉淀技术知识。用户通过提问和分享链接来学习，Claude 负责将每次对话中产生的知识精炼总结，追加到对应的分类文件中。

## 知识库分类（6 个文件）

| 文件 | 覆盖范围 |
|------|----------|
| `计算机科学.md` | 算法、数据结构、操作系统、计算机网络、编译原理、编程语言、软件工程 |
| `人工智能.md` | 机器学习、深度学习、自然语言处理、计算机视觉、强化学习、模型训练与推理 |
| `agent开发.md` | AI Agent 架构、工具调用/function calling、多 Agent 协作、RAG、LangChain 等框架 |
| `数据挖掘.md` | 自动驾驶长尾数据挖掘：EDR 触发、数据闭环、端侧推理（SA8650 NPU）、级联模型、多模态融合、规则伪标注 |
| `具身智能.md` | 机器人学、感知-行动回路、运动规划、仿真环境、SLAM、强化学习在机器人中的应用 |
| `乐理.md` | 音乐理论：音阶、和弦、节奏、和声、曲式、记谱法、乐器知识等 |

## 核心行为规则

**以下规则必须遵守，这是这个项目的存在意义：**

### 规则 1：回答问题后必须写入知识文件

每当用户提出一个涉及知识的提问，在你的回答结束后，**必须**将回答精炼为简洁的要点，追加到对应分类的 `.md` 文件中。

- 不要直接复制整段对话
- 提炼出核心概念、关键结论、技术细节
- 用最精简的语言表达，3-5 条要点通常足够

### 规则 2：分享链接后必须提取并写入

用户分享 URL 时，用 `WebFetch` 工具抓取页面内容，将页面中的核心知识提炼后追加到对应文件。

### 规则 3：追加格式与组织规则

**A. 主题归类**：同一主题的所有条目归到一个二级标题（`##`）下，按主题领域划分，例如：
- `计算机科学.md` → `## 计算机网络`、`## 数据结构`、`## 操作系统` 等
- `数据挖掘.md` → `## 车端通信`、`## 仿真数据源`、`## EDR 系统` 等

**B. 格式规范**：

- `<details open>` 默认展开，`##` 标题放入 `<summary>` 使折叠箭头在左侧
- `###` 条目用 HTML `<h3 style="color: #XXXXXX;">` 彩色标题
- 每条的"一句话总结"用 `<blockquote>` 高亮块，左边框颜色与 h3 一致，背景色为对应浅色
- 条目之间用 `---` 分隔，不标注日期
- 技术关键词用反引号 `` ` `` 标记
- 对比类内容优先用表格
- 文件顶部 `#` 标题下放置 TOC 目录链接

配色规则：

| 类型 | 色值 | 背景 |
|------|------|------|
| 理论基础 | `#2563eb` | `#f0f4ff` |
| 局限/问题 | `#d97706` | `#fffbeb` |
| 隐患/陷阱 | `#dc2626` | `#fef2f2` |
| 对比/选型 | `#7c3aed` | `#f5f3ff` |
| 系统架构 | `#059669` | `#ecfdf5` |
| 工具/平台 | `#0891b2` | `#ecfeff` |
| 通信协议 | `#4f46e5` | `#eef2ff` |

```markdown
<details open>
<summary>

## 计算机网络

</summary>

<h3 style="color: #2563eb;">TCP 与 HTTP 的关系</h3>

<blockquote style="border-left: 4px solid #2563eb; padding: 12px 16px; background: #f0f4ff; margin: 12px 0; border-radius: 0 4px 4px 0;">
💡 <strong>一句话总结</strong>：用一句通俗精炼的话概括核心结论。
</blockquote>

- 精炼的知识内容（要点形式，简洁扼要）
- 技术关键词用 `反引号` 标记

---

<h3 style="color: #d97706;">另一个主题</h3>

<blockquote style="border-left: 4px solid #d97706; padding: 12px 16px; background: #fffbeb; margin: 12px 0; border-radius: 0 4px 4px 0;">
💡 <strong>一句话总结</strong>：...
</blockquote>

- 要点

</details>
```

**C. 写入前询问**：写入文件前先告知用户，并同时给出两个选项——"写入"还是"补充后再写"。

### 规则 4：分类判断

根据内容主题判断应写入哪个文件。如果内容跨分类，写入最相关的主分类文件。如果不确定，写入最相关的那个，并在回答中告诉用户你的判断。

### 规则 5：写入前先读取

追加内容前，先用 `Read` 工具读取目标文件末尾部分（或全文，如果文件不长），确认现有内容和结尾位置，然后用 `Edit` 工具在文件末尾追加新内容。不要使用 `Write` 覆盖整个文件（那会丢失已有知识）。

### 规则 6：Git 操作规范

- **commit**：知识文件有变更时可以主动 commit，不需要每次询问用户
- **push**：commit 后直接 push（权限提示会确认），不需要用文字询问用户
- 用户可能还没有配置远程仓库，push 前先检查 `git remote -v`

## 用户特征

- 技术初学者，处于学习阶段
- 偏好解释中包含技术细节和原理，而不仅仅是操作步骤
- 偏好简洁的文件结构，不喜欢过多的小文件
- 使用中文进行交流

## 内容格式参考示例

```markdown
- [版本控制](#版本控制)

<details open>
<summary>

## 版本控制

</summary>

<h3 style="color: #2563eb;">Git 工作区、暂存区与版本库</h3>

<blockquote style="border-left: 4px solid #2563eb; padding: 12px 16px; background: #f0f4ff; margin: 12px 0; border-radius: 0 4px 4px 0;">
💡 <strong>一句话总结</strong>：工作区是你编辑的地方，暂存区是购物车，版本库是历史快照——`git add` 添加购物车，`git commit` 结算到历史。
</blockquote>

- **工作区**：你电脑上能看到的项目文件夹，编辑文件都在这里
- **暂存区**：`git add` 之后、`git commit` 之前，文件暂存的地方
- **版本库**：`git commit` 之后，文件永久保存到 `.git` 目录
- 三者关系：工作区 →(`git add`)→ 暂存区 →(`git commit`)→ 版本库

</details>
```
