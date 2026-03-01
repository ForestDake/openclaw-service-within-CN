# OpenClaw 标准版服务 - 客户检查清单

## 📋 前期准备

### 硬件要求
- [ ] macOS 设备（MacBook Pro/MacBook Air/iMac/Mac mini）
- [ ] macOS 版本 12.0+（建议 13.0+）
- [ ] 至少 8GB 内存（建议 16GB+）
- [ ] 稳定的网络连接

### 软件账号准备
- [ ] Apple ID（用于 iMessage）
- [ ] Messages.app 已登录并正常使用
- [ ] 终端应用（Terminal.app 或 iTerm2）

### API 服务账号（可选，可由客服代买）
- [ ] 阿里云百炼 API Key（推荐）
- [ ] 火山引擎 TTS API Key（可选）

---

## 🔧 安装前确认

### 网络环境检查
```bash
# 运行以下命令检查网络
curl -I https://www.baidu.com          # 国内网站
curl -I https://registry.npmmirror.com # npm 镜像
curl -I https://pypi.tuna.tsinghua.edu.cn # PyPI 镜像
```

### 系统权限提醒
安装过程中可能需要：
- [ ] 管理员密码（sudo 权限）
- [ ] Homebrew 安装授权
- [ ] 完整磁盘访问权限（iMessage 必需）

---

## 📱 iMessage 双向通讯配置

### 必须完成的权限设置

#### 步骤 1: 完整磁盘访问
1. 打开 **系统偏好设置 → 安全性与隐私 → 隐私**
2. 选择 **完整磁盘访问**
3. 点击左下角🔒解锁
4. 点击 **+** 添加终端应用
   - Terminal: `/Applications/Utilities/Terminal.app`
   - iTerm2: `/Applications/iTerm.app`
5. 勾选右侧复选框✅

#### 步骤 2: Automation 权限
1. 在左侧选择 **自动化**
2. 找到 **Messages.app**
3. 确保你的终端被勾选✅

#### 步骤 3: 重启应用
- [ ] 完全退出 Messages.app（⌘+Q）
- [ ] 重启终端应用

#### 步骤 4: 测试连接
```bash
imsg chats --limit 5 --json
```
如果返回 JSON 数据（聊天列表），说明配置成功！

---

## ✅ 安装后验证

### 功能测试清单

#### 1. OpenClaw 基础功能
```bash
# 检查 CLI 版本
openclaw --version

# 查看状态
openclaw status

# 测试技能
openclaw skills list
```

#### 2. iMessage 发送测试
```bash
# 发送测试消息给自己
imsg send --to "+86xxxxxxxxxx" --text "测试消息 - $(date)"
```

#### 3. 天气查询测试
```bash
# 测试天气技能
weather Beijing
```

#### 4. 语音合成测试
```bash
# 测试 TTS
tts "你好，我是大可，很高兴为你服务" --channel <你的通道>
```

---

## 📚 学习资源

### 官方文档
- 📖 [OpenClaw 中文文档](https://docs.openclaw.ai)
- 💻 [GitHub 仓库](https://github.com/openclaw/openclaw)
- 💎 [Gitee 镜像](https://gitee.com/openclaw-china/openclaw)

### 技能文档
每个技能的详细用法在 `SKILL.md` 中，例如：
```bash
cat /opt/homebrew/lib/node_modules/openclaw/skills/imsg/SKILL.md
```

---

## 🔧 常见问题自查

| 问题 | 可能原因 | 解决方法 |
|------|---------|---------|
| `imsg chats` 权限错误 | 未授予完整磁盘访问 | 见上方 iMessage 配置 |
| `npm install` 超时 | 网络问题 | 已自动配置国内镜像 |
| `openclaw` 命令找不到 | PATH 未生效 | 重启终端 |
| API Key 报错 | 余额不足/格式错误 | 联系技术支持 |

---

## 📞 技术支持

### 服务范围（标准版 ¥499）
- ✅ 远程安装部署
- ✅ iMessage 双向通讯配置
- ✅ 预设 5 个基础技能
- ✅ 1 小时讲解培训
- ✅ 7 天免费咨询

### 联系方式
- 📱 微信：[待填写]
- 📧 邮箱：[待填写]
- ⏰ 支持时间：9:00-21:00（工作日）

### 响应时效
- 紧急情况：30 分钟内响应
- 普通问题：2 小时内响应
- 非工作时间：次日 9:00 后处理

---

## 📝 交付确认

安装完成后请确认：

- [ ] 终端可正常启动
- [ ] `openclaw` 命令可用
- [ ] imsg 能发送消息
- [ ] 工作区文件正确生成
- [ ] 已阅读基本文档
- [ ] 理解日常使用方法

**签字确认：** _______________  **日期：** ___________

---

*这份清单由 OpenClaw 中国服务团队提供 © 2026*
