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

## 实操记录

### 2026-10-10 首次打通全流程

| 步骤 | 内容 | 结果 |
|---|---|---|
| 1 | 修复 Git 全局身份 | `gf92syt8kj-arch <336407470+gf92syt8kj-arch@users.noreply.github.com>` |
| 2 | 生成 SSH 密钥 | `~/.ssh/id_ed25519`（ed25519） |
| 3 | 公钥登记到 GitHub | `Hi gf92syt8kj-arch! You've successfully authenticated` |
| 4 | 本地提交 | `b412f08` on `main` |
| 5 | 推送到远程 | `* [new branch] main -> main` |

### 本次排查的一个真实问题

浏览器打不开 GitHub，但 SSH 推送正常。诊断结论：

- `github.com` 被 DNS 解析到 `20.205.243.166`
- 该 IP 的 **443 端口超时**，而 **22 端口正常** → 所以网页挂、推送好
- 其他 GitHub 边缘 IP（`140.82.113.3` 等）的 443 全部正常

修复思路：GitHub 边缘按 SNI 路由，把 `github.com` 指向任意一台可连通的边缘 IP
即可，详见同目录的 `fix-github-hosts.sh`。

**经验**：网页打不开不等于网络不通，要分开测 DNS、端口、以及不同 IP，
才能定位到是"单个 IP 坏了"而不是"整体被墙"。
