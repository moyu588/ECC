# ECC 汉化 Fork 维护指南

> 本仓库（moyu588/ECC）是 affaan-m/ECC 的 fork，在官方 v2.2.1 基础上汉化了
> 94 个 commands 与 51 个 skills 的 description（见提交 `00f7caaa`）。
> 汉化内容只保留在本 fork，不推送回上游源仓库。

## 仓库关系

```
affaan-m/ECC（上游，原作者仓库，只读）
      │  fetch upstream
      ▼
moyu588/ECC（本 fork，main = 上游内容 + 汉化提交）
      │  git clone / 插件安装
      ▼
各台 PC 的本地副本
```

单分支策略：汉化提交直接落在 `main`，不另建分支。

## 一、新 PC 安装（每台一次性）

在 Claude Code 中执行：

```
/plugin marketplace add https://github.com/moyu588/ECC.git
/plugin install ecc@ecc
```

安装完成即为汉化版。重启 Claude Code 会话后生效。

## 二、上游更新合并（固定三条命令）

上游有新版本时，在服务器的本地仓库（`/openclaw/github/ECC`）执行：

```bash
cd /openclaw/github/ECC
git fetch upstream && git merge upstream/main   # 汉化提交原样保留
git push origin main
```

- 若 merge 提示冲突：说明上游改了某个已汉化的文件，
  处理原则是「保留上游新内容 + 重新翻译成中文」，逐个解决后
  `git add <文件> && git commit` 再推送。
- **禁止**使用 GitHub 网页的 "Sync fork" 按钮：出现
  "Discard XX commits" 提示时会删除汉化提交。
- 本机 `upstream` 远程的 push 地址已禁用
  （`DISABLED-no-push-to-upstream`），无法误推汉化到源仓库。

合并推送后，各台 PC 在 Claude Code 中执行以下命令拉取最新：

```
/plugin marketplace update
```

## 三、汉化内容更新

1. 在本地仓库修改对应文件（`commands/*.md`、`skills/*/SKILL.md` 的 frontmatter description）
2. `git add -A && git commit -m "docs: 汉化 <范围>" && git push origin main`
3. 各台 PC 执行 `/plugin marketplace update`

## 附：服务器环境备忘

| 项 | 值 |
|---|---|
| 本地工作仓库 | `/openclaw/github/ECC` |
| origin | `git@github.com:moyu588/ECC.git`（SSH，账户级 key：`~/.ssh/id_openclaw-sec-alert`） |
| upstream | `https://github.com/affaan-m/ECC.git`（仅 fetch，push 已禁用） |
| 提交身份 | `moyu588 <moyu588@users.noreply.github.com>`（仅本仓库生效） |
| 汉化基线 | 上游 v2.2.1（commit `e04ea0b`），汉化提交 `00f7caaa` |
