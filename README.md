# Skills

我的 Agent Skills 集合，适用于 Claude Code、OpenClaw 等 AI 助手。

## 怎么安装

单个 skill 安装：

```bash
npx skills add zhengzhuangpro/skills --skill [skillname]
```

全部安装：

```bash
npx skills add zhengzhuangpro/skills -g --yes --all
```

## Skills 列表

| Skill 名称 | 说明 |
| --- | --- |
| tool-site-design-system | 开发者工具产品的落地页 |

## 怎么创建新 Skill

1. 复制模板：`cp -r skills/_template skills/your-skill-name`
2. 编辑 `SKILL.md`（给 Claude 看的指令）
3. 编辑 `README.md`（给人看的说明）
4. 更新本文件的 Skills 列表
