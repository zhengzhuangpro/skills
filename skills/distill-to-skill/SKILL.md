---
name: distill-to-skill
description: |
  把用户在别处写的内容（笔记、聊天记录、文档、博客、随手记）提炼成本仓库规范的 skill。
  触发词：提炼 skill, 总结成 skill, 做成 skill, 写成 skill, distill to skill
---

# distill-to-skill

## 指令正文

你的任务：把用户提供的素材提炼成 `zhengzhuangpro/skills` 仓库中一个规范的新 skill。

### 1. 定位仓库

本 skill 的产出目录是 skills 仓库（`zhengzhuangpro/skills`）。如果当前目录不是该仓库，先找到或 clone 它，所有操作都在该仓库内进行。

### 2. 收集并理解素材

- 素材来源不限：粘贴的文本、文件路径、URL、聊天记录、笔记。
- 通读全部素材后再动手。素材里有含糊或矛盾的地方，先向用户确认，不要猜。

### 3. 提炼（核心步骤）

提炼的是**可复用的方法和判断标准**，不是原文存档：

- 问自己：用户以后遇到什么类似任务时，会希望 Claude 按这套方式做？
- 保留：流程步骤、判断依据、取舍原则、检查清单、用户明确的偏好。
- 丢弃：一次性的上下文、具体项目细节、寒暄和过程性内容。
- 如果素材里隐含了用户的工作习惯（比如"先问再做"、"输出要简洁"），把它写成明确指令。

### 4. 命名

- 英文 kebab-case，从内容本质出发（如 `distill-to-skill`）。
- 素材主题不必符合仓库现有 skill 的主题——本仓库是通用集合，任何可复用的方法都可以进来。

### 5. 创建文件

```bash
cp -r skills/_template skills/<skill-name>
```

**SKILL.md**（给 Claude 看）：

- frontmatter 的 `description` 写清楚"做什么 + 什么时候触发"，触发词贴近用户平时的说法。
- 指令正文用祈使句、步骤化，每一步可直接执行，不写空话。

**README.md**（给人看）：

- 一句话说明 + 安装命令 + 使用示例（用户会对 Claude 说的原话）。

### 6. 收尾

1. 更新仓库根目录 `README.md` 的 Skills 列表，加一行。
2. 提交：`feat: 新增 <skill-name> skill`，不加任何 AI 署名尾注。
3. 告诉用户：说"更新"即可发布并全局安装。
