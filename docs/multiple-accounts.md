# 本机 GitHub 多账号使用指南

## 查看与切换

```bash
gh auth status
gh auth switch --hostname github.com --user bcblr1993
gh api user --jq .login
```

需要使用另一个已登录账号时，将用户名换成对应账号。操作前用最后一条命令确认身份。

## HTTPS 认证

```bash
gh auth setup-git --hostname github.com
```

这会让 Git HTTPS 使用 GitHub CLI 的凭据。它不改变 SSH 认证，也不自动更改仓库 remote URL。

## 提交作者

在目标仓库目录中查看配置：

```bash
git config --get user.name
git config --get user.email
git remote -v
```

如需更改作者，只设置当前仓库，避免影响其他项目：

```bash
git config --local user.name "你的 GitHub 用户名"
git config --local user.email "GitHub 设置页面提供的邮箱"
```

邮箱可使用 GitHub Settings → Emails 中提供的 noreply 地址。登录身份决定访问权限，提交作者决定提交归属，两者应分别核对。

## 提交前检查

```bash
git status --short
git diff --check
git diff --cached
```

只暂存需要提交的文件。PR 合并前检查差异与项目要求的测试结果。

## 常见问题

- **Repository not found**：检查当前账号、仓库地址及该账号的访问权限。
- **作者显示不正确**：检查提交邮箱是否关联目标账号；切换登录不能修正已有提交。
- **徽章没有出现**：作者关联正确和 PR 已合并不等于成就已发放，仍需查看个人主页。

参考：[GitHub CLI auth switch](https://cli.github.com/manual/gh_auth_switch)、[auth setup-git](https://cli.github.com/manual/gh_auth_setup-git)。
