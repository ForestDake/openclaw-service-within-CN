# OpenClaw 中国版 - 快速开始指南

<div align="center">

🤖 **你的私人 AI 助手，本地运行，数据可控**

[![版本](https://img.shields.io/badge/版本 -1.0-blue.svg)]()
[![系统](https://img.shields.io/badge/系统-macOS-green.svg)]()
[![语言](https://img.shields.io/badge/语言 - 中文-red.svg)]()

</div>

---

## 📖 目录

- [什么是 OpenClaw？](#什么是-openclaw)
- [核心功能](#核心功能)
- [一键安装](#一键安装)
- [配置 iMessage](#配置-imessage)
- [常用命令](#常用命令)
- [服务套餐](#服务套餐)
- [常见问题](#常见问题)

---

## 什么是 OpenClaw？

OpenClaw 是一个开源的 AI 助手框架，让你能在本地设备上运行个性化的智能助手：

```
┌─────────────────────────────────────────────┐
│  你 (MacBook Pro / iPhone / iPad)           │
│      ↓                                      │
│  OpenClaw (本地运行)                         │
│      ↓                                      │
│  LLM API + 各种技能工具                       │
│      ↓                                      │
│  iMessage / Webchat / Email...              │
└─────────────────────────────────────────────┘
```

### 为什么选择 OpenClaw？

| 优势 | 说明 |
|------|------|
| 🔒 **隐私可控** | 所有数据处理在本地，只有 API 调用需要联网 |
| 🚀 **高度定制** | 按需开发技能，满足各种场景需求 |
| 💰 **成本透明** | 只需支付 API 调用费，软件完全免费 |
| 🎯 **深度集成** | 与 macOS 原生应用无缝协作（备忘录、提醒等） |

---

## 核心功能

### 📨 iMessage 双向通讯

```bash
# 发送消息
imsg send --to "+861xxxxxxxxx" --text "你好！"

# 查看聊天记录
imsg history --chat-id 1 --limit 20
```

**支持的场景**:
- ✅ 每日金融日报自动推送
- ✅ 日程提醒通知
- ✅ 重要事件告警
- ✅ 随时语音交互

### 🌤️ 天气查询

```bash
weather Beijing
weather "Shanghai, CN" --units celsius
```

### 📝 苹果笔记管理

```bash
memo add "买牛奶和面包" --library 日常
memo search "购物清单"
```

### ⏰ 提醒事项

```bash
remindctl add "下午 3 点开会" --list 工作 --date today 15:00
```

### 📊 更多技能

- `weather` - 全球天气查询
- `apple-notes` - 苹果备忘录 CRUD
- `apple-reminders` - 提醒事项管理
- `healthcheck` - 系统安全诊断
- `pdf-convert` - PDF 格式转换
- `video-frames` - 视频帧提取
- ... 以及更多可自定义的技能

---

## 一键安装

### 方式一：官方脚本（推荐）

```bash
# 下载并执行安装脚本
curl -fsSL https://example.com/openclaw-install-cn.sh | bash
```

### 方式二：手动安装

#### 1. 安装 Homebrew

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

#### 2. 配置国内镜像

```bash
export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.aliyun.com/homebrew/bottles
```

#### 3. 安装依赖和 OpenClaw

```bash
brew install node python@3.11 sqlite jq
npm install -g openclaw
brew install steipete/tap/imsg
```

#### 4. 验证安装

```bash
openclaw --version
imsg --version
```

---

## 配置 iMessage

iMessage 双向通讯是 OpenClaw 的核心功能之一，需要配置系统权限：

### 步骤 1: 完整磁盘访问

1. 打开 **系统偏好设置 → 安全性与隐私 → 隐私**
2. 选择 **完整磁盘访问**
3. 点击左下角🔒解锁
4. 点击 **+** 添加终端应用
5. 勾选右侧复选框✅

### 步骤 2: Automation 权限

1. 在左侧选择 **自动化**
2. 找到 **Messages.app**
3. 确保 Terminal/iTerm2 被勾选✅

### 步骤 3: 测试连接

```bash
imsg chats --limit 5 --json
```

如果返回 JSON 数据（聊天列表），说明配置成功！

---

## 常用命令

### 基础操作

```bash
# 查看状态
openclaw status

# 更新软件
openclaw update

# 查看帮助
openclaw --help

# 清理缓存
openclaw cache clean
```

### 技能使用

```bash
# 天气
weather Shanghai

# 发送 iMessage
imsg send --to "+86xxx" --text "测试消息"

# 创建笔记
memo add "任务内容" --library 工作

# 查看提醒
remindctl list
```

### 定时任务

```bash
# 编辑 crontab
crontab -e

# 每天 9 点执行
0 9 * * * cd ~/ && openclaw run daily-financial-report
```

---

## 服务套餐

我们提供专业的远程安装和配置服务：

| 套餐 | 价格 | 服务内容 |
|------|------|---------|
| **入门版** | ¥199 | 基础安装 + 文档指导 |
| **标准版** | ¥499 | 完整配置 + iMessage 双向 + 培训 +7 天支持 |
| **专业版** | ¥999 | 定制技能 + 长期跟进 |

**标准版包含**:
- ✅ 远程部署到可用
- ✅ iMessage 双向通讯配置
- ✅ 预装 5 个基础技能
- ✅ 1 小时培训讲解
- ✅ 7 天免费咨询
- ✅ 完整交付文档

---

## 常见问题

### Q: API Key 费用大概多少？

**A:** 取决于使用频率，个人用户一般在 ¥50-200/月：
- 阿里云百炼：¥0.01-0.1/次（根据模型）
- 火山引擎 TTS: 有免费额度
- 具体用量可以在后台查看

### Q: 数据安全吗？

**A:** 
- ✅ 所有文件存储在你自己的 Mac 上
- ✅ iMessage 记录不上传第三方服务器
- ⚠️ API 调用内容会被 LLM 服务商处理（这是必须的）
- ⚠️ 可以选择国内大模型降低风险

### Q: 能帮我做哪些事情？

**A:** 典型场景：
- 每天早上推送金融新闻和股市行情
- 接收日历提醒和待办事项
- 语音对话控制智能家居
- 自动生成日报/周报
- 自定义任何你能想到的自动化流程

### Q: 没有编程经验能学会吗？

**A:** 
- 基础使用（查天气、发消息）→ 看半天教程即可
- 进阶使用（写脚本、定时任务）→ 1-2 周可以上手
- 高级使用（开发技能）→ 需要有 Shell/Python 基础

我们有详细的中文文档和视频教程，即使是小白也能快速上手。

---

## 📞 联系我们

**技术咨询**: GitHub @ForestDake  
**微信服务**: （扫码或搜索）  
**工作时间**: 9:00-21:00

---

## 📄 许可证

OpenClaw 采用 MIT 开源协议。商业服务部分另行约定。

© 2026 OpenClaw 中国服务团队

---

<div align="center">

**如果你觉得这个项目有用，欢迎推荐给朋友！** ⭐

</div>
