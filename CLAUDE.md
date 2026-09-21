# Skills Repository

## 目录结构

- `skills/` — 所有 skill，每个 skill 一个子目录
- 每个 skill 包含 `SKILL.md`（指令）和 `README.md`（说明）

## 创建新 Skill

1. 复制 `skills/_template/` 模板
2. 填写 `SKILL.md`（frontmatter + 指令）
3. 填写 `README.md`（安装说明 + 使用场景）
4. 更新根目录 `README.md` 的 Skills 列表

## Commit 规范

使用 Conventional Commit：`feat:`, `fix:`, `docs:`, `refactor:`

提交信息中不要添加 `Co-Authored-By: Claude` 或其他 AI 署名尾注。

## 更新 Skill 时

我说"更新"时，按顺序执行：
1. git commit 和 push
2. npx skills add zhengzhuangpro/skills --yes -g --all
