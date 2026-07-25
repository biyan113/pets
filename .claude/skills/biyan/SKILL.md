---
name: biyan
description: 以 biyan 身份配置当前项目的 git 用户名/邮箱并发布到 GitHub (账号 biyan113)。当用户说"发布到 github"、"用 biyan 提交"、"biyan 发布"、"配置 biyan 账号"、"推送到 github"等,或显式调用 /biyan 时触发。会设置项目级 user.name=biyan / user.email=gpt123@panw3i.com,切换 gh 到 biyan113 账号,提交变更并创建 public 仓库推送。
---

# biyan — 以 biyan 身份发布当前项目到 GitHub

将当前项目以 **biyan** 的身份提交并发布到 GitHub 账号 **biyan113**。

## 固定身份

| 项 | 值 |
|---|---|
| Git 用户名 | `biyan` |
| Git 邮箱 | `gpt123@panw3i.com` |
| GitHub 账号 | `biyan113` |
| 仓库可见性 | `public`（除非用户另行指定） |
| 配置作用域 | **项目级**（`git config` 不带 `--global`，绝不污染全局配置） |

## 执行流程

严格按顺序执行，每一步都判断当前状态，跳过已完成的部分。

### 1. 切换 GitHub CLI 账号到 biyan113

```bash
gh auth switch --user biyan113 && gh api user --jq '.login'
```

- 输出应为 `biyan113`。若该账号未登录，提示用户先 `gh auth login` 登录 biyan113。

### 2. 设置项目级 Git 身份

在**项目根目录**执行（必须是 `git config`，不能是 `git config --global`）：

```bash
git config user.name  "biyan"
git config user.email "gpt123@panw3i.com"
git config user.name && git config user.email   # 回显确认
```

### 3. 初始化仓库（仅当尚未 init）

```bash
git rev-parse --is-inside-work-tree 2>/dev/null || git init -b main
```

- 已是 git 仓库则跳过；否则 `git init -b main`。
- 若项目缺 `.gitignore`，按项目类型补一个最小 `.gitignore`（至少排除 `.DS_Store`）。

### 4. 暂存并提交变更（仅当有变更）

```bash
git add -A
git status --porcelain | head   # 查看待提交内容
```

- 若无变更且已有提交 → 跳过 commit，直接进入第 5 步推送。
- 若有变更 → 提交，commit message 用**简体中文**概括本次改动，结尾追加：

  ```
  Co-Authored-By: Claude <noreply@anthropic.com>
  ```

  示例：
  ```bash
  git commit -m "$(cat <<'EOF'
  更新素材:新增挥手状态帧

  Co-Authored-By: Claude <noreply@anthropic.com>
  EOF
  )"
  ```

### 5. 创建 GitHub 仓库并推送

**仓库名**：取当前目录名（`basename "$PWD"`），除非用户指定其它名字。

先判断远程是否已存在：

```bash
git remote get-url origin 2>/dev/null
```

- **远程不存在**（首次发布）：

  ```bash
  gh repo create <仓库名> --public --source=. --push \
    --description "<一句话项目描述，中文>"
  ```

  描述优先从项目内容（README 首行 / package.json / 现有清单）归纳；无法归纳时让用户提供。

- **远程已存在**（后续更新）：

  ```bash
  git push -u origin HEAD
  ```

  如远程有本地的 fetch 未合并，先与用户确认再 `--force`，绝不擅自强推。

### 6. 输出结果

推送成功后，回显仓库地址：

```
✅ 已发布:https://github.com/biyan113/<仓库名>
```

## 约束与边界

- **作用域**：所有 `git config` 必须是项目级。绝不修改 `~/.gitconfig` 或全局身份。
- **可见性**：默认 `--public`。用户明确要求 private 时改 `--private` 并复述确认。
- **不擅自强推**：`git push --force` 需用户确认。
- **仓库名冲突**：若 `gh repo create` 报已存在，提示用户选择改名或推送到已有仓库，不覆盖远程。
- **账号隔离**：发布前务必确认 `gh api user` 返回 `biyan113`，避免误推到其它账号。
