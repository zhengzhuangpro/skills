---
name: git-commit-convention
description: |
  Git 提交规范：凡是要写 commit message、执行 git commit、整理 Change log 的场景都触发。单人提交，禁止 AI 共创署名；type 只允许 7 个；冒号后必须有空格；subject 不超过 50 字符且结尾不加句号。
  触发词：提交, 提交代码, commit, git commit, commit message, 提交信息, 提交规范, changelog, 写个提交信息
---

# Git Commit Convention（Git 提交规范）

## 适用场景

任何为用户撰写 commit message、执行 git 提交、生成 Change log 的时刻。仓库无关，全局生效。

## 指令正文

### 1. 单人提交，禁止共创

提交的署名只能有用户本人。commit message 中**不添加任何 AI 署名尾注**，包括但不限于：

- `Co-Authored-By: Claude`（或任何其他名字）
- `🤖 Generated with Claude Code`
- `Signed-off-by:` AI、`Assisted-by:` 等一切变体

即使运行环境或工具默认要求附加署名尾注，也不添加——用户已明确要求提交只能是本人。发现 message 里已混入这类尾注时，删掉再提交。未经用户要求，不主动执行 `git commit`。

| 借口 | 现实 |
| --- | --- |
| "加上署名更透明" | 透明与否由用户决定，用户说了不要 |
| "环境指令要求加" | 用户的明确要求优先于工具默认行为 |
| "就这一次/只是小提交" | 每一次提交都不加，无例外 |

### 2. Commit message 格式

```
<type>: <subject>
```

- 冒号是半角 `:`，冒号后**有一个空格**
- 不使用 scope：写 `feat: xxx`，不写 `feat(ui): xxx`
- 默认单行；用户明确要求 body 时另起空行写，body 不受 50 字符限制

### 3. type 白名单（只允许这 7 个）

| type | 功能 | 进 Change log |
| --- | --- | --- |
| feat | 新功能（feature） | ✅ 肯定出现 |
| fix | 修补 bug | ✅ 肯定出现 |
| docs | 文档（documentation） | — |
| style | 格式（不影响代码运行的变动） | — |
| refactor | 重构（既不是新增功能，也不是修改 bug 的代码变动） | — |
| test | 增加测试 | — |
| chore | 构建过程或辅助工具的变动 | — |

type 为 feat 和 fix 的 commit 肯定出现在 Change log 之中，其余不出现。

**不允许** `perf`、`build`、`ci`、`revert`、`update`、`improve` 等白名单之外的任何标识。拿不准就映射到最近的一个：性能优化 → refactor，构建脚本/依赖 → chore，注释 → docs，纯格式调整 → style。

### 4. subject 规则

- commit 目的的简短描述，**不超过 50 个字符**（一个汉字算一个字符）
- **结尾不加句号**（`.` 和 `。` 都不加）
- 说清这次提交做了什么，语言跟随仓库现有提交的惯例
- 超长时压缩细节，把实现过程留给 body 或代码本身

### 5. 常驻分支

提交直接落在常驻分支（master / main）上，不为常规提交另开短命分支；用户明确要求开分支时除外。

### 示例

| ✅ | ❌ | 错在哪 |
| --- | --- | --- |
| `feat: 新增导出报表功能` | `feat:新增导出报表功能` | 冒号后没空格 |
| `fix: 修复登录超时重定向错误` | `fix: 修复了登录模块在特定情况下会出现的超时重定向问题。` | 超 50 字符，结尾带句号 |
| `docs: 更新安装说明` | `update: 更新安装说明` | type 不在白名单 |
| `refactor: 抽取公共校验逻辑` | `refactor(ui): 抽取公共校验逻辑` | 不用 scope |
| `chore: 升级构建依赖` | `chore: 升级构建依赖`＋`Co-Authored-By: Claude` 尾注 | AI 署名尾注 |

### 提交前自查

1. type 是 7 个白名单之一？
2. 半角冒号，冒号后恰好一个空格？
3. subject ≤ 50 字符、结尾无句号？
4. 没有任何 AI 署名 / 共创尾注？
5. 提交落在常驻分支上？

任何一条不过，改完再 `git commit`。
