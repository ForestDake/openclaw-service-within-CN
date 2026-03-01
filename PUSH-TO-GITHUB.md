# 推送到 GitHub 操作指南

## 📋 快速步骤

### 方式一：手动操作（推荐）

#### 1. 在 GitHub 创建仓库

1. 访问 https://github.com/new
2. Repository name: `openclaw-cn-service` (或其他你喜欢的名字)
3. Description: `OpenClaw 中国版标准服务包 - 一键安装和配置工具`
4. 选择 **Public** 或 **Private**
5. ❌ 不要勾选 "Add README"、".gitignore"、"license"（我们已经有了）
6. 点击 **"Create repository"**

#### 2. 关联远程仓库并推送

```bash
cd /Users/qicao/.openclaw/workspace/business

# 替换 <你的 GitHub 用户名> 为 ForestDake
git remote add origin https://github.com/ForestDake/openclaw-cn-service.git

# 推送代码
git push -u origin main

# 如果默认分支是 master 而不是 main
# git branch -M main
# git push -u origin main
```

---

### 方式二：使用 GitHub CLI（如果你已安装 gh）

```bash
cd /Users/qicao/.openclaw/workspace/business

# 创建仓库并推送
gh repo create ForestDake/openclaw-cn-service --public --source=. --push
```

---

## ✅ 验证提交是否成功

推送完成后，访问：
```
https://github.com/ForestDake/openclaw-cn-service
```

你应该能看到以下文件：

```
📁 .gitignore
📄 CHECKLIST.md
📄 DELIVERY-TEMPLATE.md
📄 FAQ.md
📄 INDEX.md
📄 POST-INSTALL-GUIDE.md
📄 PRE-INSTALL-QUESTIONS.md
📄 README-CN.md
📝 openclaw-install-cn.sh (可执行)
```

---

## 🔒 安全确认

已删除的个人信息：
- ✅ 手机号 (+8615026714798) → 替换为占位符 (+86xxxxxxxxxx)
- ✅ 邮箱 (caoqi1874@outlook.com) → 替换为 GitHub 账号 (@ForestDake)
- ✅ API Key 示例 → 仅保留占位符格式 (sk-xxxxxx)

无真实敏感信息可以公开分享！✅

---

## 📢 发布后建议

### 1. 更新 README

可以考虑添加一个更详细的 README.md（从 README-CN.md 转换），包括：

```markdown
# OpenClaw 中国版服务包

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
```

### 2. 设置 GitHub Pages（可选）

如果想做成在线文档：
- Settings → Pages → Source: main branch / root
- 会生成 https://forestdake.github.io/openclaw-cn-service/

### 3. 开源许可

如果需要添加 LICENSE 文件，可以：
```bash
cd /Users/qicao/.openclaw/workspace/business
echo "MIT License - See LICENSE file" >> README-CN.md
```

---

## 🆘 遇到问题？

### 问题：权限被拒绝

```bash
# 解决方法：使用 SSH 密钥
ssh-keygen -t ed25519 -C "ForestDake@users.noreply.github.com"
# 复制 ~/.ssh/id_ed25519.pub 内容到 GitHub Settings → SSH keys
git remote set-url origin git@github.com:ForestDake/openclaw-cn-service.git
```

### 问题：分支名不是 main

```bash
git branch -m main
git push -u origin main
```

### 问题：推送失败

```bash
# 检查认证
gh auth status  # 如果安装了 GitHub CLI

# 或使用 Personal Access Token
git remote set-url origin https://<PAT>@github.com/ForestDake/openclaw-cn-service.git
```

---

完成以上步骤后，你的项目就成功发布到 GitHub 了！🎉
