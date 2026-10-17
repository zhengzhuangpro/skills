# git-commit-convention

Git 提交规范（Conventional Commit 精简版）：

- 单人提交——不添加 `Co-Authored-By: Claude` 等任何 AI 共创署名
- 格式 `<type>: <subject>`，冒号后必须有空格
- type 只允许 7 个：`feat` / `fix` / `docs` / `style` / `refactor` / `test` / `chore`（feat、fix 进 Change log）
- subject 不超过 50 个字符，结尾不加句号
- 提交落在常驻分支（master / main）上

## 安装

```bash
npx skills add zhengzhuangpro/skills --skill git-commit-convention
```

## 使用

安装后，Claude 在任何提交代码的场景自动应用本规范，无需手动触发。也可以直接说"看看这个提交信息合不合规范"让它检查。

## 详细文档

查看 [SKILL.md](./SKILL.md) 了解完整指令。
