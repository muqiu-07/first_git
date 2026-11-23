# first_git

我的第一个 Git 练习仓库，用来熟悉 `git init` → `git add` → `git commit` 的完整流程。

## 这个仓库里有什么

- `README.md` —— 就是你正在看的这份说明

## 我在这个仓库练过的命令

```bash
git init                       # 初始化仓库
git status                     # 查看当前状态
git add .                      # 把所有改动放进暂存区
git commit -m "first commit"   # 提交到本地仓库
git log --oneline              # 查看提交历史
git remote -v                  # 查看远程仓库地址（push 之前务必核对）
git push -u origin main        # 首次推送，-u 记住跟踪关系
git push                       # 之后只需这两个词
```

## 踩坑备忘

### 1. push 报 `Invalid username or token`

不一定是你密码错了。先检查有没有代理改写了 GitHub 地址：

```bash
git config --global --get-regexp "url\."
```

如果看到 `insteadOf https://github.com/` 这样的规则，说明请求被转发到了中转站，GitHub 根本收不到认证信息。删掉它：

```bash
git config --global --unset url.https://gh-proxy.com/https://github.com/.insteadof
```

另外 GitHub 从 2021 年起不接受账号密码推送，只认 Personal Access Token 或浏览器 OAuth 授权。

### 2. 只想下载时借用加速，不要全局开

`push` 涉及认证，走中转必失败。需要加速 `clone` 时用单次参数，别写进全局配置：

```bash
git -c url.https://gh-proxy.com/https://github.com/.insteadof=https://github.com/ clone https://github.com/用户名/仓库名.git
```

### 3. 远程地址填错了仓库

`git remote add` 之后、`git push` 之前，永远先看一眼：

```bash
git remote -v
```

地址里的仓库名必须和当前项目一致。填错时删除重加：

```bash
git remote remove origin
git remote add origin https://github.com/用户名/正确的仓库名.git
```

### 4. 远程仓库建的时候勾了 README

本地推送会被拒绝（`fetch first`）。先合并再推：

```bash
git pull --rebase origin main
git push
```

## 备注

- 默认分支：`main`
- 远程仓库：https://github.com/muqiu-07/first_git
- 提交身份：`muqiu-07 <muqiu-07@users.noreply.github.com>`
