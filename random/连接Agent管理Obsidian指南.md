---
type: guide
created: 2026-04-28
tags: [Obsidian, Git, Agent]
---
# 连接Agent管理Obsidian指南

## 前提条件
- Obsidian仓库已创建
- GitHub账号
- iCloud同步已配置（iPhone + Windows）

## 步骤一：创建GitHub私有仓库

1. 登录 GitHub → 右上角 `+` → `New repository`
2. 仓库名随意（如 `feishu-agent-vault`）
3. 选择 **Private**
4. 点击 `Create repository`

## 步骤二：生成Personal Access Token

1. 点右上角头像 → `Settings`
2. 左侧菜单拉到最下面 → `Developer settings`
3. 选 `Personal access tokens` → `Fine-grained tokens`
4. 点 `Generate new token`
5. 填写：
   - Token name：随意，如 `obsidian`
   - Expiration：选90天或更长
   - Repository access：选 `Only select repositories` → 选你的仓库
   - Permissions → Repository permissions → `Contents` 选 `Read and write`
6. 点 `Generate token`
7. **复制token（只显示一次）**

## 步骤三：将Token和仓库地址发给Agent

把以下信息发给Agent：
- 仓库地址：`https://github.com/用户名/仓库名.git`
- Personal Access Token

Agent会将这些信息安全保存，之后即可远程管理仓库。

## 步骤四：本地仓库推送到GitHub

在Windows终端执行：

```bash
cd "iCloud Drive/Obsidian/你的仓库名"
git init
git remote add origin https://github.com/用户名/仓库名.git
git add .
git commit -m "init vault"
git push -u origin main
```

## 步骤五：配置Obsidian Git插件（自动同步）

1. Obsidian → 设置 → 第三方插件 → 浏览 → 搜索 `Obsidian Git`
2. 安装并启用
3. 设置自动同步间隔（建议10分钟）
4. 开启自动pull和自动push

## 使用方式

- **Agent操作**：告诉Agent要做什么，它会通过GitHub API修改仓库，你设备自动pull
- **你操作**：正常在Obsidian里编辑，Git插件自动push，Agent下次操作时能拿到最新

## 同步流程

```
Agent改GitHub → 你设备自动pull → Obsidian更新
你改Obsidian → Git插件自动push → Agent下次clone能拿到最新
```

## 注意事项

- 不要同时在多端编辑同一篇笔记，避免冲突
- Token过期后需要重新生成并更新给Agent
- 建议定期检查Git同步状态，确保不卡住
