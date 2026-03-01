# OpenClaw 安装后使用指南

## 🎉 欢迎！

恭喜你已经成功安装 OpenClaw！这份指南将帮助你在第一周快速上手。

---

## 📅 第一周学习路线

### Day 1: 初次接触

#### 1. 验证安装状态
```bash
# 检查所有组件是否正常
openclaw status
openclaw --version

# 查看已安装的技能
ls ~/.openclaw/workspace/skills/
```

#### 2. 配置你的身份信息
编辑 `~/.openclaw/workspace/IDENTITY.md`:
```markdown
- **Name:** [你的名字]
- **Creature:** AI 助手
- **Vibe:** 温暖、专业
- **Emoji:** 🤖
- **Language:** 中文
- **Role:** 智能个人助理
```

#### 3. 填好用户信息
编辑 `~/.openclaw/workspace/USER.md`:
```markdown
- **Name:** [客户姓名]
- **iMessage:** +86xxxxxxxxxx
- **邮箱:** xxx@xxx.com
```

#### 4. 测试 iMessage（如果已配置权限）
```bash
# 给自己发条消息
imsg send --to "+86xxxxxxxxxx" --text "OpenClaw 安装完成，开始测试！"
```

---

### Day 2-3: 熟悉基础功能

#### 天气查询
```bash
# 查询北京天气
weather Beijing

# 带单位查询
weather Shanghai --units celsius

# 输出示例：
# 🌤️ 上海当前天气: 多云, 22°C
# 今日最高/最低: 25°C / 18°C
```

#### 苹果备忘录
```bash
# 创建一条新笔记
memo add "买牛奶和面包" --library 日常

# 搜索笔记
memo search "购物"

# 列出所有笔记
memo list
```

#### 苹果提醒事项
```bash
# 添加提醒
remindctl add "下午 3 点开会" --list 工作 --date today 15:00

# 查看所有待办
remindctl list
```

---

### Day 4-5: 了解核心概念

#### 什么是 SOUL.md？
```markdown
SOUL.md 定义了 AI 的人格设定：
- 性格特点
- 交流风格
- 行为边界
```

**建议阅读时间**: 30 分钟  
**重点理解**: 不要问重复的问题，要自己先尝试解决

#### 什么是 MEMORY.md？
```markdown
MEMORY.md 是长期记忆存储：
- 重要决策记录
- 用户偏好
- 技能成长历史
```

**如何使用**: 
- AI 会自动学习并更新这个文件
- 你也可以手动添加重要信息

#### 什么是 HEARTBEAT.md？
```markdown
HEARTBEAT.md 定义定期检查任务：
- 每天检查邮件
- 查看日历
- 天气提醒
```

**自定义检查内容**:
```markdown
# 你可以在这里添加自己的检查项
- [ ] 上午 9 点检查股票行情
- [ ] 下午 6 点检查小红书画报
```

---

### Day 6-7: 进阶使用

#### 设置定时任务

**场景**: 每天早上 9 点发送金融日报

1. **编辑 crontab**
   ```bash
   crontab -e
   ```

2. **添加规则**
   ```bash
   # 每天 9 点执行
   0 9 * * * cd /Users/yourname && openclaw run financial-daily
   ```

或者在 `config.yaml` 中配置：
```yaml
cron:
  - name: "daily-financial"
    schedule: "0 9 * * *"
    command: "/path/to/script.sh"
```

#### 自定义工作流程

**例子**: 一键生成日报

```bash
#!/bin/bash
# ~/bin/daily-report.sh

echo "=== 金融新闻 ===" >> /tmp/report.txt
curl https://example.com/finance | grep "<title>" >> /tmp/report.txt

echo "=== 天气预报 ===" >> /tmp/report.txt
weather Beijing >> /tmp/report.txt

echo "=== 日程提醒 ===" >> /tmp/report.txt
calendar tomorrow >> /tmp/report.txt

# 发送到 iMessage
cat /tmp/report.txt | imsg send --to "+86xxxxxxxxxx" --file -
```

---

## 🛠️ 高级技巧

### 1. 使用环境变量管理敏感信息

```bash
# ~/.zshrc
export OPENCLAW_API_KEY="sk-xxx"
export VOLCANO_TTS_KEY="xxx"
```

然后在 config.yaml 中使用：
```yaml
provider:
  llm:
    api_key: "${OPENCLAW_API_KEY}"
```

### 2. 日志追踪

```bash
# 实时查看日志
tail -f ~/.openclaw/logs/app.log

# 查看最近的错误
grep ERROR ~/.openclaw/logs/*.log | tail -20
```

### 3. 快速重启服务

```bash
# 重启网关
openclaw gateway restart

# 清空缓存
rm -rf ~/.openclaw/cache/*

# 重新加载配置
source ~/.zshrc
```

### 4. 备份重要数据

```bash
# 创建备份脚本
cat > ~/backup-openclaw.sh << 'EOF'
#!/bin/bash
DATE=$(date +%Y%m%d)
tar czf ~/backups/openclaw-$DATE.tar.gz \
    ~/.openclaw/workspace \
    ~/.openclaw/config.yaml
echo "备份完成：openclaw-$DATE.tar.gz"
EOF

chmod +x ~/backup-openclaw.sh
```

---

## 📱 iMessage 深度使用

### 监听新消息

如果你想让 AI 自动回复你的 iMessage：

```bash
# 找到你的聊天 ID
imsg chats --limit 20 --json | jq '.[] | select(.phone_number == "+86xxxxxxxxxx")'

# 使用 chat_id (假设是 1)
imsg watch --chat-id 1 --attachments
```

### 批量发消息

```bash
# 给多个联系人发相同消息
for phone in "+861xxxx" "+862xxxx" "+863xxxx"; do
    imsg send --to "$phone" --text "新年快乐！"
    sleep 2  # 防止被 Spam 检测
done
```

---

## 🎨 个性化定制

### 更换 AI 模型

编辑 `config.yaml`:
```yaml
provider:
  llm:
    type: "moonshot"      # 或 zhipu, deepseek, etc.
    model: "moonshot-v1-8k"
    temperature: 0.7       # 更creative
```

### 调整语音合成声音

```yaml
provider:
  tts:
    voice: "nova"         # ElevenLabs 的 Nova 声音
    speed: 1.0            # 语速
```

### 自定义提示词

在 `workspace/PROMPTS.md` 中添加：
```markdown
## 角色设定
你是一位专业的金融分析师，擅长：
- 解读财经新闻
- 分析股市趋势
- 给出投资建议（仅供参考）

## 语气要求
- 专业但不刻板
- 多用图表和数据说话
- 对风险要明确提示
```

---

## 🔧 故障排查

### 问题 1: imsg 突然不能用了

**症状**: `permission denied` 或无法读取聊天记录

**解决方案**:
```bash
# 1. 重置 TCC 权限
tccutil reset All com.apple.Terminal

# 2. 完全退出 Messages.app
killall Messages

# 3. 重启终端
exec zsh

# 4. 再次测试
imsg chats --limit 5 --json
```

### 问题 2: API Key 报错 401

**症状**: "Unauthorized" 或 "Invalid API Key"

**解决方案**:
```bash
# 1. 检查环境变量
echo $OPENCLAW_API_KEY

# 2. 检查 config.yaml 中的 Key
cat ~/.openclaw/config.yaml | grep api_key

# 3. 登录阿里云百炼控制台检查余额
```

### 问题 3: 内存占用过高

**症状**: Mac 变卡，内存显示 90%+

**解决方案**:
```bash
# 1. 查找占用进程
ps aux | grep node | head -10

# 2. 清理旧会话
openclaw sessions cleanup --older-than 7d

# 3. 重启网关
openclaw gateway restart
```

---

## 📚 持续学习

### 推荐阅读顺序

1. **入门级**
   - [ ] `AGENTS.md` - 了解基本规则
   - [ ] `SOUL.md` - 理解人格设定
   - [ ] 官方文档简介

2. **进阶级**
   - [ ] 各技能的 SKILL.md
   - [ ] 配置文件详解
   - [ ] Shell 脚本入门

3. **专家级**
   - [ ] 开发自定义技能
   - [ ] 深入理解架构
   - [ ] 性能优化

### 社区资源

- 📖 官方文档：https://docs.openclaw.ai
- 💬 Discord 社区: https://discord.gg/clawd
- 💻 GitHub: https://github.com/openclaw/openclaw
- 🏠 Gitee 镜像: https://gitee.com/openclaw-china

---

## 🆘 需要帮助？

### 自助排查

```bash
# 运行诊断脚本
openclaw diagnostics

# 收集系统信息
openclaw info --output json

# 生成报告发给技术支持
openclaw support-bundle --output report.json
```

### 联系支持

- 📧 邮箱：GitHub @ForestDake
- 📱 微信：_________________
- ⏰ 工作时间：9:00-21:00

**联系时请准备**:
1. macOS 版本 (`sw_vers`)
2. OpenClaw 版本 (`openclaw --version`)
3. 具体问题和错误截图
4. 相关的日志片段

---

*祝你使用愉快！🎉*

*最后更新: 2026-03-01 | OpenClaw 中国服务团队*
