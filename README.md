# github-practice

这是我用来跑通 Git + GitHub 全流程的练习仓库。

## 它验证了什么

- 本地 Git 仓库的初始化（`git init`）
- 暂存与提交（`git add` / `git commit`）
- 提交者身份是否正确绑定到 GitHub 账号
- 通过 SSH 推送到远程仓库（`git push`）

## 三个位置的对照

| 位置 | 在哪 | 怎么到达 |
|---|---|---|
| 工作区 | 你正在编辑的文件 | —— |
| 本地仓库 | `.git` 目录，在你自己硬盘上 | `git add` → `git commit` |
| 远程仓库 | GitHub 服务器 | `git push` ↑ / `git pull` ↓ |

**关键点**：`commit` 只写进本地仓库，不会上传。只有 `push` 才会到 GitHub。

## 常用命令

```bash
git status                 # 看当前改了什么
git diff                   # 看具体改动内容
git add .                  # 暂存全部改动
git commit -m "说明"        # 提交到本地
git push                   # 推送到 GitHub
git pull                   # 拉取远程更新
git log --oneline --graph  # 查看提交历史
```
