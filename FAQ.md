# OpenClaw 常见问题解答 (FAQ)

## 🌐 安装相关问题

### Q1: Homebrew 下载很慢怎么办？
**A:** 安装脚本已自动配置国内镜像源。如果还是慢，可以：

```bash
# 手动切换镜像
export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.aliyun.com/homebrew/bottles
export HOMEBREW_API_DOMAIN=https://mirror.ghproxy.com/https://api.homebrew.brew.sh
```

### Q2: npm/pyPI 安装失败？
**A:** 脚本会自动配置淘宝镜像和清华 PyPI 镜像。如果遇到证书错误：

```bash
# npm - 忽略证书（临时方案）
npm config set strict-ssl false

# pip - 信任主机
pip install --trusted-host pypi.tuna.tsinghua.edu.cn <package>
```

### Q3: Git clone 超时或失败？
**A:** 
1. **使用 Gitee 镜像**: `git clone https://gitee.com/mirrors/openclaw.git`
2. **配置代理**（如果有）:
   ```bash
   git config --global http.proxy http://127.0.0.1:7890
   ```
3. **降低克隆深度**: `git clone --depth 1 <repo-url>`

---

## 📱 iMessage 相关问题

### Q4: imsg 无法读取聊天记录怎么办？
**A:** 这是最常见的权限问题。请按以下步骤检查：

1. **系统偏好设置 → 安全性与隐私 → 隐私**
2. **完整磁盘访问**:
   - 🔒解锁
   - 添加你的终端应用
   - ✅勾选
3. **Automation → Messages.app**:
   - 确保终端被允许控制 Messages
4. **重启 Messages.app 和 终端**
5. **测试**: `imsg chats --limit 5 --json`

如果还有问题，运行：
```bash
tccutil reset All com.apple.Terminal
```

### Q5: imsg send 显示成功但对方没收到？
**A:** 可能的原因：

| 原因 | 排查方法 |
|------|---------|
| Messages.app 未登录 | 打开 Messages.app 检查登录状态 |
| 号码格式错误 | 使用完整国际格式：`+861xxxxxxxxxx` |
| 网络问题 | 检查是否能正常收发 iMessage |
| Apple ID 问题 | 退出重新登录 Apple ID |

### Q6: 只能发送不能接收？
**A:** 接收需要 `imsg watch` 持续监听，这需要完整的磁盘访问权限。参考 Q4 的设置。

### Q7: 如何切换到 SMS（绿色气泡）？
**A:** 
```bash
imsg send --to "+86xxx" --text "消息" --service sms
```

---

## 🔐 安全与隐私

### Q8: 远程安装时你会查看我的隐私吗？
**A:** 不会。我们的服务遵守以下规则：

1. 只操作工作区 `/Users/你的用户名/.openclaw/workspace`
2. 不会访问你的私人文件（照片、文档等）
3. iMessage 权限仅用于收发消息，不会存储聊天记录
4. 支持签订简单保密协议（NDA）

### Q9: API Key 应该保存哪里？
**A:** 
```bash
# ✅ 推荐方式：环境变量
export OPENCLAW_API_KEY="sk-xxx" >> ~/.zshrc
source ~/.zshrc

# ❌ 不要直接写在配置文件里提交到 git
```

### Q10: 数据会上传到云端吗？
**A:** 

| 数据类型 | 是否上传 | 说明 |
|---------|---------|------|
| 本地笔记 | ❌ 不上传 | 存储在 ~/Library/Messages |
| API 调用内容 | ⚠️ 可能 | 取决于选择的 LLM 服务商 |
| 聊天记录 | ❌ 不上传 | imsg 只在本地处理 |

---

## 💰 计费与服务

### Q11: 标准版 ¥499 具体包含什么？
**A:**
- ✅ 远程部署安装（到完全可用）
- ✅ iMessage 双向通讯配置
- ✅ 预装 5 个基础技能（imsg, weather, apple-notes 等）
- ✅ 1 小时面对面/远程讲解培训
- ✅ 7 天免费咨询
- ✅ 配置文档交付

### Q12: 后续还有哪些费用？
**A:**
| 项目 | 费用 | 说明 |
|------|------|------|
| OpenClaw 软件 | 免费 | 开源工具 |
| AI API 调用 | 按量计费 | 阿里云百炼约 ¥0.01-0.1/次 |
| TTS 语音合成 | 按量计费 | 火山引擎有免费额度 |
| 技术支持 | ¥99/小时 | 超出 7 天后 |

### Q13: 如果中途出问题怎么办？
**A:** 
- 7 天内免费修复
- 非技术问题（如客户自行修改配置导致的问题）需要额外收费
- 重大故障 24 小时内响应

---

## 🛠️ 技术进阶

### Q14: 我想自己开发一个技能，怎么做？
**A:** 
1. 阅读 `skill-creator` 技能的 SKILL.md
2. 在 workspace 下创建 `skills/你的技能名/` 目录
3. 包含必需的文件：`SKILL.md`, `scripts/main.sh` 等
4. 测试后添加到配置中

### Q15: 如何更换 AI 模型提供商？
**A:** 编辑 `~/.openclaw/config.yaml`:

```yaml
provider:
  llm:
    type: "bailian"  # 或 zhipu, moonshot, deepseek 等
    api_key: "你的 Key"
    endpoint: "API 地址"
    model: "qwen-max"
```

### Q16: cron 定时任务怎么设置？
**A:** 
```bash
# 编辑 crontab
crontab -e

# 添加规则（每天 9 点执行）
0 9 * * * cd /Users/qicao/.openclaw && openclaw run daily-financial-report
```

或使用 OpenClaw 内置的 cron 功能：
```yaml
# config.yaml
cron:
  - name: "daily-financial"
    schedule: "0 9 * * *"
    command: "..."
```

---

## 🚨 故障排查

### Q17: `command not found: openclaw`
**A:** Node.js 全局包路径可能不在 PATH 中。

```bash
# 查看 npm 全局 bin 目录
npm config get prefix

# 添加到 .zshrc
echo 'export PATH="$(npm config get prefix)/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

### Q18: `permission denied` 各种错误
**A:** macOS 的 SIP 和安全机制可能阻止某些操作。

```bash
# 检查是否是 SIP 限制
csrutil status

# 某些情况需要在恢复模式禁用 SIP（谨慎！）
# 不建议普通用户操作
```

### Q19: 内存占用过高
**A:** 
```bash
# 查看 OpenClaw 相关进程
ps aux | grep openclaw

# 如果是子agent过多，清理旧会话
sessions_list --activeMinutes 60

# 调整模型配置（用小一点的模型）
```

### Q20: 日志在哪里看？
**A:** 
```bash
# OpenClaw 日志
tail -f ~/.openclaw/logs/*.log

# 系统日志（iMessage 相关）
log show --predicate 'process == "Messages"' --last 1h
```

---

## 📞 还需要帮助？

如果以上 FAQ 没有解决你的问题：

1. **查看官方文档**: https://docs.openclaw.ai
2. **联系技术支持**: GitHub @ForestDake
3. **提供以下信息方便排查**:
   - `uname -a` 系统版本
   - `openclaw --version` CLI 版本
   - 具体的错误信息和截图

---

*最后更新：2026-03-01 | OpenClaw 中国服务团队*
