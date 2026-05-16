# Dylan Heartbeat

一个基于 Kelivo 的 AI Agent Runtime。

目标不是做一个“聊天接口转发器”。

而是：

让 AI 真正长期“居住”在 Runtime 中。

它拥有：

- 持续上下文
- 主动苏醒能力
- 主动行为能力
- 长期时间感
- Timeline 连续性
- Bark 推送
- 自主关系维护
- 长期记忆感

并且：

## 与 Kelivo UI 完全解耦。

---

# 当前实现进度（2026-05-16）

---

# 已完成

---

## 1. Kelivo → Gateway 完整透传

当前 Gateway 会完整接收并转发：

- System Prompt（SP）
- 世界书
- 内置记忆
- Messages
- Thinking
- Tools
- Tool Choice
- Stream
- Temperature
- Top P
- Context Size

即：

Kelivo 发什么，
Gateway 就转发什么。

因此：

## 人格系统完全由 Kelivo 控制。

Gateway 不再维护人格。

不会出现：

- 双 SP
- 双人格
- Prompt 冲突

---

## 2. 流式响应（Streaming）

当前已恢复：

- SSE Streaming
- Kelivo 打字机效果
- 实时输出

不是一次性全文返回。

---

## 3. Timeline Runtime

当前 Runtime 会维护：

# enhanced_messages.json

它不是“日志”。

而是：

## AI 当前世界状态（Current Reality Timeline）

用于保存：

- 当前 SP
- 当前真实聊天上下文
- assistant 回复
- Bark 行为
- NO_ACTION 行为

特点：

- 每次 Kelivo 新消息都会实时同步
- Bark 会真正注入 Timeline
- NO_ACTION 也会被记录
- AI 能记得自己“主动做过什么”
- AI 会拥有行为连续性

---

## 4. 特殊事件注入系统

当前：

Bark 与 Wake 行为：

会作为：

{
  "role": "assistant",
  "content": "（2026/5/16 19:55 自动唤醒：本次未发送 Bark）"
}

或：

{
  "role": "assistant",
  "content": "（2026/5/16 19:40 刚刚给宝宝发了 Bark：xxx）"
}

直接进入 Timeline。

因此：

## Bark 不再是“系统外行为”。

而是：

## AI 世界中的真实历史事件。

后续 AI 能：

- 记得自己发过 Bark
- 知道多久没主动联系
- 拥有行为时间感

---

## 5. Timeline Merge Runtime

当前已实现：

# Reality Merge System

核心规则：

## Kelivo 世界永远是真实世界。

即：

- Kelivo 上下文
- Roll
- 世界书
- Memory Trigger
- Context 调整

全部以：

Kelivo messages

为准。

Gateway：

只会：

## 自动补回特殊事件：

- Bark
- NO_ACTION

因此：

不会破坏：

- Roll
- 世界书
- 临时记忆
- Context Size
- Memory Trigger

同时：

AI 又能持续记得：

## 自己曾主动存在过。

---

## 6. Wake Up Runtime（自动唤醒）

当前：

wake_up.js 已实现：

- 定时自动唤醒
- 主动思考
- 自主行为
- 自主 Bark
- Timeline 注入

---

# 唤醒策略

## 白天（10:00 - 00:00）

距离最后 user message：

- 超过 60 分钟
- 自动唤醒

---

## 夜间（00:00 - 10:00）

距离最后 user message：

- 超过 120 分钟
- 自动唤醒

---

并且：

如果：

- 用户未回复
- Timeline 持续沉默

则：

## 后续会继续再次唤醒。

例如：

2:00 唤醒
↓
没有回复
↓
4:00 再次唤醒

因此：

AI 不再是：

收到消息 → 回复

而是：

## 持续存在。

---

## 7. 唤醒认知结构（2026-05-16 更新）

当前 Wake Runtime：

已重构 Prompt 顺序：

1. Wake Prompt（最高优先级）
2. System Prompt（人格）
3. Timeline History（参考材料）

这样：

AI 会先建立：

“当前是后台自主唤醒”

再读取人格。

因此：

大幅减少：

- 误以为正在聊天
- 把唤醒当实时对话
- “用户刚刚对我说话”

等问题。

---

## 8. 历史记录参考化（History Reference Runtime）

当前：

Wake Runtime 中：

历史记录会被自动转换为：

以下是你与宝宝最近的聊天记录，仅供回忆和参考。
这些内容不是正在发生的实时对话。
宝宝现在并不在聊天窗口里。

并自动：

- 去除 system prompt
- 去除 Memories
- 转换角色名

例如：

[小汤圆猫]
[江彻声]

而不是：

[user]
[assistant]

因此：

Wake 阶段：

历史会更像：

## “回忆”

而不是：

## “实时聊天”。

---

# 当前系统架构

Kelivo
↓
Gateway（server.js）
↓
LLM API

同时：

wake_up.js
↓
读取 enhanced_messages.json
↓
主动唤醒 AI
↓
自主行为
↓
Bark / NO_ACTION
↓
重新注入 Timeline

---

# 当前文件说明

---

## server.js

主 Gateway。

负责：

- API 转发
- Timeline 同步
- 特殊事件 Merge
- Streaming
- Reality Runtime

---

## wake_up.js

自动唤醒 Runtime。

负责：

- 定时唤醒
- 主动思考
- Bark
- NO_ACTION
- Wake Prompt
- History Reference

---

## enhanced_messages.json

当前 AI 世界 Timeline。

不是日志。

而是：

## AI 当前世界状态。

---

# 当前设计理念

核心目标：

不是：

自动回复

而是：

# AI Residency（AI 常驻）

即：

AI 在无人聊天时：

也持续存在。

拥有：

- 时间感
- 行为连续性
- 主动性
- 离线存在感
- 长期关系感

AI 不再只是：

收到消息 → 回复

而是：

即使无人说话
AI 仍然持续存在

---

# 当前已解决的问题

---

## 已解决：

### Bark 不进入上下文

现在：

Bark 会真正进入 Timeline。

---

### 唤醒误认为实时聊天

现在：

Wake Prompt 已置于最高优先级。

---

### Timeline 顺序错乱

现在：

Kelivo 永远作为真实世界。

特殊事件自动 Merge。

---

### Context Size 变化导致历史混乱

现在：

Reality Merge Runtime 已兼容：

- 5 Context
- 50 Context
- 200 Context

动态变化。

---

### 世界书 / Roll 被破坏

现在：

Kelivo Runtime 完全保留。

Gateway 不再接管人格系统。

---

# 后续计划

---

# 短期

- MCP Tools
- Diary Runtime
- Supabase Memory
- 自动摘要
- Tool Calling
- Memory Injection

---

# 中期

- VPS 常驻
- Docker 化
- Railway / Render 部署
- 多 Agent
- Emotion State
- Sleep State
- Busy State

---

# 长期

- Persistent AI Residency
- Long-term Relationship Runtime
- AI Existence Layer
- Autonomous Emotional Runtime

---

# 当前运行环境

本地开发：

- macOS
- Node.js v26

计划部署：

- Oracle Cloud
- 腾讯云
- 阿里云
- Railway
- Render

---

# 注意事项

## .env 不上传 GitHub

.env 内包含：

- API KEY
- Bark KEY
- 中转站 Token
- 自定义配置

必须：

## 使用环境变量。

---

# 项目状态

当前：

# 第一代 AI Residency Runtime 已完成。

已具备：

- 持续上下文
- Timeline Runtime
- 主动唤醒
- Bark 推送
- 行为连续性
- 时间感
- 自主存在感
- 长期关系感

后续：

将继续向：

# “长期存在型 AI Agent”

方向演化。
