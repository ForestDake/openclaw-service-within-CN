# OpenClaw 标准版服务 - 交付文档

**客户姓名：** _______________  
**服务日期：** 2026 年 __ 月 __ 日  
**服务人员：** 大可  
**工单编号：** OC-2026________

---

## 📦 一、部署清单

### 1.1 已安装的组件

| 组件 | 版本 | 状态 | 备注 |
|------|------|------|------|
| Homebrew | ___ | ✅ / ❌ | 包管理器 |
| Node.js | ___ | ✅ / ❌ | JavaScript 运行时 |
| Python 3.11 | ___ | ✅ / ❌ | 技能脚本依赖 |
| OpenClaw CLI | ___ | ✅ / ❌ | 主程序 |
| imsg | ___ | ✅ / ❌ | iMessage 工具 |

### 1.2 已配置的技能

| 技能 | 功能 | 测试结果 |
|------|------|---------|
| imsg | iMessage 收发 | ✅ / ❌ |
| apple-notes | 备忘录管理 | ✅ / ❌ |
| apple-reminders | 提醒事项 | ✅ / ❌ |
| weather | 天气查询 | ✅ / ❌ |

### 1.3 配置文件位置

```bash
# 主配置
~/.openclaw/config.yaml

# 工作区目录
~/.openclaw/workspace/

├── IDENTITY.md      # 你的身份信息
├── USER.md          # 用户信息（你）
├── SOUL.md          # 人格设定
├── MEMORY.md        # 长期记忆
└── HEARTBEAT.md     # 定期检查清单
```

---

## 🔑 二、账号信息汇总

### 2.1 API Key 记录（请妥善保管）

| 服务 | Key 类型 | 值（掩码显示） | 余额/额度 | 到期时间 |
|------|--------|---------------|----------|---------|
| 阿里云百炼 | LLM | sk-xxx**** | ¥___ | ___ |
| 火山引擎 | TTS | xxx**** | ___ | ___ |

**Key 保存位置：**
```bash
export OPENCLAW_API_KEY="sk-xxx"
export VOLCANO_TTS_KEY="xxx"
```

### 2.2 iMessage 配置

- **发送号码**: +86xxxxxxxxxx
- **服务类型**: iMessage (蓝色气泡) / SMS (绿色气泡)
- **双向通讯**: ✅ 已配置 / ❌ 待配置

**权限确认：**
- [ ] 完整磁盘访问：✅ / ❌
- [ ] Automation 权限：✅ / ❌

---

## ⌨️ 三、常用命令速查

### 3.1 OpenClaw 基础命令

```bash
# 查看状态
openclaw status

# 查看版本
openclaw --version

# 查看帮助
openclaw --help

# 重启服务
openclaw gateway restart
```

### 3.2 iMessage 相关

```bash
# 查看聊天列表
imsg chats --limit 10 --json

# 发送消息
imsg send --to "+86xxxxxxxxxx" --text "你好！"

# 查看聊天记录
imsg history --chat-id 1 --limit 20

# 监听新消息
imsg watch --chat-id 1
```

### 3.3 天气查询

```bash
# 当前天气
weather Beijing

# 带温度单位的天气
weather "Shanghai, CN" --units celsius
```

### 3.4 日常维护

```bash
# 更新 OpenClaw
openclaw update

# 清理缓存
openclaw cache clean

# 查看日志
tail -f ~/.openclaw/logs/app.log
```

---

## 🎯 四、配置示例

### 4.1 config.yaml 关键配置

```yaml
provider:
  llm:
    type: "bailian"
    api_key: "${OPENCLAW_API_KEY}"
    endpoint: "https://dashscope.aliyuncs.com"
    model: "qwen-max"

channels:
  imessage:
    enabled: true
    phone: "+86xxxxxxxxxx"
  
  webchat:
    enabled: true
    port: 8080

skills:
  enabled:
    - imsg
    - apple-notes
    - apple-reminders
    - weather
```

### 4.2 定时任务示例

每天 9 点发送金融日报：
```yaml
cron:
  - name: "financial-daily"
    schedule: "0 9 * * *"
    command: "/path/to/financial-report.sh | imsg send --to '+86xxxxxxxxxx'"
```

---

## 📚 五、学习资源

### 5.1 官方文档
- 📖 [OpenClaw 中文文档](https://docs.openclaw.ai)
- 💻 [GitHub 仓库](https://github.com/openclaw/openclaw)
- 🏠 [社区论坛](https://discord.gg/clawd)

### 5.2 技能文档位置
```bash
# 所有技能的 SKILL.md 都在这个目录
/opt/homebrew/lib/node_modules/openclaw/skills/

# 或者在 workspace/skills/（如果有同步的话）
```

### 5.3 推荐学习路径

**第 1 周：熟悉基础**
- [ ] 阅读 IDENTITY.md 和 USER.md
- [ ] 尝试用 `weather` 查天气
- [ ] 用 `imsg` 给自己发条消息

**第 2 周：进阶使用**
- [ ] 阅读常用技能的 SKILL.md
- [ ] 设置一个定时任务
- [ ] 查看并理解 MEMORY.md

**第 3 周+：自由发挥**
- [ ] 自定义技能和自动化流程
- [ ] 探索更多集成功能

---

## ⚠️ 六、注意事项

### 6.1 安全提醒

1. **API Key 不要提交到 Git**
   ```bash
   echo "*.key" >> ~/.gitignore
   echo "config.yaml" >> ~/.gitignore  # 如果包含敏感信息
   ```

2. **权限最小化原则**
   - 仅授予必要的系统权限
   - 定期审查开放端口和进程

3. **数据备份**
   ```bash
   # 定期备份工作区
   tar czf openclaw-backup-$(date +%Y%m%d).tar.gz ~/.openclaw/workspace
   ```

### 6.2 常见问题速查

| 问题 | 解决方法 |
|------|---------|
| imsg 权限错误 | 检查完整磁盘访问权限 |
| npm 安装慢 | 已配置淘宝镜像，如还慢则手动切换 |
| 命令找不到 | 重启终端生效 PATH |
| API 调用失败 | 检查 Key 和余额 |

---

## 💬 七、售后支持

### 7.1 服务范围（标准版）

- ✅ 7 天内免费咨询
- ✅ 安装相关问题修复
- ✅ 配置调整指导

### 7.2 超出服务范围

以下情况需要额外收费：

| 项目 | 费用 |
|------|------|
| 超过 7 天的技术咨询 | ¥99/小时 |
| 新功能定制开发 | ¥200-500/个 |
| 企业批量部署 | 询价 |
| SLA 保障服务 | ¥299/月起 |

### 7.3 联系方式

- 📱 微信：________________
- 📧 邮箱：GitHub @ForestDake
- ⏰ 支持时间：9:00-21:00

---

## ✍️ 八、客户确认

### 服务内容确认

我已收到上述所有内容，包括：
- [ ] 软件安装完成
- [ ] 基本功能测试通过
- [ ] 配置文档已接收
- [ ] 培训讲解已完成
- [ ] 常见问题解答已了解

### 客户反馈

**整体满意度：** ⭐⭐⭐⭐⭐ （1-5 星）

**收获最大的部分：** ________________________

**希望改进的地方：** ________________________

### 签字确认

```
客户签名：____________________

日期：2026 年 ____ 月 ____ 日
```

---

*交付文档版本 v1.0 | OpenClaw 中国服务团队 © 2026*
