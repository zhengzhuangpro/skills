# Skills

我的 Agent Skills 集合，适用于 Claude Code、OpenClaw 等 AI 助手。

## Skills 列表

| Skill 名称 | 说明 |
| --- | --- |
| tool-site-design-system | 开发者工具产品的落地页 |
| distill-to-skill | 把别处写的内容提炼成仓库规范的 skill |

## 怎么安装

从远程安装：

```bash
npx skills add zhengzhuangpro/skills --skill [skillname]
```

全部安装：

```bash
npx skills add zhengzhuangpro/skills -g --yes --all
```

从本地安装（clone 到本地后）：

```bash
npx skills add ./skills -g --yes --all
```

## Fork 后自己用

如果你想基于这个仓库定制自己的 skills：

```bash
# 1. Fork 仓库到你的 GitHub

# 2. 克隆你的 fork
git clone git@github.com:你的用户名/skills.git
cd skills

# 3. 添加上游仓库（可选，方便同步更新）
git remote add upstream git@github.com:zhengzhuangpro/skills.git

# 4. 安装你自己的 skills
npx skills add 你的用户名/skills -g --yes --all

# 5. 后续同步上游更新
git fetch upstream
git merge upstream/master
```

## 怎么创建新 Skill

1. 复制模板：`cp -r skills/_template skills/your-skill-name`
2. 编辑 `SKILL.md`（给 Claude 看的指令）
3. 编辑 `README.md`（给人看的说明）
4. 更新本文件的 Skills 列表
