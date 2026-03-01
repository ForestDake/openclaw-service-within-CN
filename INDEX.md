# OpenClaw 标准版服务 - 文件索引

## 📁 目录结构

```
business/
├── INDEX.md                           # 本文档 - 文件索引
├── openclaw-install-cn.sh            # 🔧 一键安装脚本（核心）
├── PRE-INSTALL-QUESTIONS.md          # 📋 客户预沟通问卷
├── CHECKLIST.md                      # ✅ 客户检查清单
├── FAQ.md                            # ❓ 常见问题解答
├── DELIVERY-TEMPLATE.md              # 📦 交付文档模板
├── POST-INSTALL-GUIDE.md             # 📚 安装后使用指南
└── README-CN.md                      # 📘 中文快速开始手册
```

---

## 📄 各文件说明

| 文件名 | 用途 | 何时使用 |
|--------|------|---------|
| **openclaw-install-cn.sh** | 自动安装脚本 | 远程协助时让客户先运行，或作为现场演示工具 |
| **PRE-INSTALL-QUESTIONS.md** | 需求收集问卷 | 预约服务前发给客户填写 |
| **CHECKLIST.md** | 准备清单 | 安装前发给客户自查 |
| **FAQ.md** | 问题解答 | 客户咨询问题时参考 |
| **DELIVERY-TEMPLATE.md** | 交付文档 | 安装完成后填充具体内容给客户 |
| **POST-INSTALL-GUIDE.md** | 使用教程 | 交付后指导客户学习 |
| **README-CN.md** | 宣传手册 | 推广用，可做成 PDF 发给潜在客户 |

---

## 🚀 快速上手流程

### 第一次接触潜在客户

1. **发送 README-CN.md** 让他们了解这是什么
2. **询问是否需要服务** → 如果有意向
3. **发送 PRE-INSTALL-QUESTIONS.md** 收集需求和设备信息
4. **根据反馈报价** → 确认套餐和价格
5. **约定时间** → 准备远程会议

### 服务当天

1. **提前 5 分钟** 联系客户确认
2. **先发 CHECKLIST.md** 让客户提前看一遍
3. **连接远程桌面** （向日葵/ToDesk）
4. **让客户运行 openclaw-install-cn.sh** 
   ```bash
   curl -fsSL /path/to/openclaw-install-cn.sh | bash
   ```
5. **边安装边讲解** 每步在做什么
6. **配置 iMessage 权限** 这是最难的部分
7. **现场测试功能** 确保都能正常使用
8. **填充 DELIVERY-TEMPLATE.md** 生成正式交付文档
9. **发送 POST-INSTALL-GUIDE.md** 告诉客户后续怎么学

### 服务结束后

1. **加微信拉群** 方便后续咨询
2. **7 天内主动跟进** 问有没有遇到问题
3. **记录到 MEMORY.md** 把经验沉淀下来

---

## 💡 使用建议

### 给脚本添加执行权限

```bash
chmod +x openclaw-install-cn.sh
```

### 可以自定义的地方

| 位置 | 如何修改 |
|------|---------|
| 安装包价格 | `READM-CN.md` + `DELIVERY-TEMPLATE.md` |
| 支持联系方式 | 所有文件中的联系方式字段 |
| 默认技能列表 | `openclaw-install-cn.sh` 的 `install_skills()` 函数 |
| API Key 推荐渠道 | `FAQ.md` 的费用部分 |

### 可以自动化生成的内容

```bash
#!/bin/bash
# generate-delivery-doc.sh - 自动生成交付文档

DATE=$(date +%Y%m%d)
CUSTOMER="张三"

cp DELIVERY-TEMPLATE.md "delivery-$CUSTOMER-$DATE.md"

sed -i "" "s/_______________/$CUSTOMER/g" "delivery-$CUSTOMER-$DATE.md"
sed -i "" "s/2026 年 __ 月 __ 日/2026 年 $(date +%m 月 %d 日)/g" "delivery-$CUSTOMER-$DATE.md"
sed -i "" "s/________/$(date +%H%M)/g" "delivery-$CUSTOMER-$DATE.md"

echo "交付文档已生成：delivery-$CUSTOMER-$DATE.md"
```

---

## 🎯 定价策略建议

### 入门版 ¥199（引流款）
**目标**: 降低尝试门槛  
**限制**: 
- 仅远程安装，不包含深度配置
- iMessage 单向发送（不监听回复）
- 无培训时间
- 24 小时内响应

### 标准版 ¥499（主力款）⭐
**目标**: 性价比最优  
**包含**:
- 完整安装配置
- iMessage 双向通讯
- 基础技能培训
- 7 天免费咨询

### 专业版 ¥999（利润款）
**目标**: 高价值客户  
**增值**:
- 定制 2-3 个专属技能
- 2 小时深度培训
- 30 天跟进服务
- 每月一次巡检

### 企业版 询价
**目标**: B 端批量部署  
**特色**:
- 多台机器统一配置
- 内部培训
- SLA 保障
- 源码托管在私有仓库

---

## 📊 成本核算

### 直接成本

| 项目 | 单次费用 | 备注 |
|------|---------|------|
| 远程软件会员 | ¥0-50/月 | 向日葵免费版够用 |
| 屏幕录制软件 | ¥0-30/月 | OBS 免费 |
| API Key 代购差价 | 成本+10% | 如果需要代购 |
| 交通成本 | ¥0 | 纯远程 |

### 时间成本

| 环节 | 时长 | 频率 |
|------|------|------|
| 前期沟通 | 15-30 分钟 | 每次 |
| 远程安装 | 45-90 分钟 | 标准版 |
| 培训讲解 | 30-60 分钟 | 标准版 |
| 售后咨询 | 5-15 分钟 | 平均每天 |

### 净利润估算

**按标准版 ¥499 计算：**
- 收入：¥499
- 直接成本：¥10（间接支出）
- 时间成本：~2 小时 × ¥50 = ¥100
- **毛利润：~¥389 (78%)**

如果一个月做 10 单：
- 总收入：¥4,990
- 总工时：~20 小时
- **时薪：~¥195**

---

## 🔗 外部资源

### 官方文档
- https://docs.openclaw.ai
- https://github.com/openclaw/openclaw

### 镜像源地址
- Homebrew: https://mirrors.tuna.tsinghua.edu.cn/homebrew/bottles
- npm: https://registry.npmmirror.com
- PyPI: https://pypi.tuna.tsinghua.edu.cn/simple

### 国内 API 服务商
- 阿里云百炼: https://bailian.aliyun.com
- 火山引擎 TTS: https://www.volcengine.com/product/VoiceConsole
- 智谱 AI: https://open.bigmodel.cn
- Moonshot AI: https://platform.moonshot.cn

---

## ⚠️ 注意事项

### 法律合规
1. 明确告知客户 AI 使用范围，不要用于违法场景
2. API 调用内容可能需要符合当地法规
3. 建议签署简单的服务条款

### 技术边界
1. 写清楚服务范围，超出的要额外收费
2. 不负责解决非本软件引起的问题（如系统崩溃）
3. 数据备份责任归属要明确

### 隐私保护
1. 远程时避免查看客户私人文件
2. 可以要求签署保密协议（NDA）
3. 不保留客户的任何敏感信息

---

## 📈 持续优化方向

### 短期（1-3 个月）
- [ ] 录制视频教程（脱敏后公开）
- [ ] 建立常见问题的快捷回复库
- [ ] 开发更多定制化技能模板

### 中期（3-6 个月）
- [ ] 制作标准化的培训 PPT
- [ ] 开发自助式 Web 安装向导
- [ ] 建立客户案例库

### 长期（6 个月+）
- [ ] 考虑 SaaS 化的配置管理后台
- [ ] 探索企业级批量部署方案
- [ ] 建立合作伙伴网络

---

*文档版本：v1.0 | 最后更新：2026-03-01 | OpenClaw 中国服务团队*
