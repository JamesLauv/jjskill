---
name: jjskill
description: Personal work artifact router for James/JJ. Trigger: /jjskill, jjskill, JJ Skill, 工作流主入口, 帮我看看, 整理一下. Use when the user provides project materials, meeting notes, customer requirements, sales/pre-sales content, technical evaluations, internal communication drafts, or scattered business documents and asks to 整理, 分析, 帮我看看, 做成沟通材料, 生成决策材料, 推进表, 方案对比, 汇报材料, choose an output format, or route the work to the right jjskill-* workflow such as jjskill-doc-to-decision-artifacts.
---

# JJ Skill 主入口

这是个人工作流路由 Skill。用于判断用户给出的材料或任务应该进入哪类 `jjskill-*` 工作流。

## 路由原则

如果用户明确指定具体任务，直接进入对应 Skill。

如果用户表达比较模糊，比如：

- “帮我看看这个材料”
- “整理一下方便沟通”
- “做成能跟团队讲的东西”
- “这个怎么推进”
- “帮我输出成表格/HTML/飞书文档”
- “这个客户需求怎么拆”

先判断任务类型，再进入具体 Skill。

## 当前可路由 Skill

### jjskill-doc-to-decision-artifacts

用于把项目文档、技术评估、会议纪要、需求草稿等材料，通过交互共创，整理成可沟通、可决策、可推进的材料。

适用场景：

- 方案评估
- 决策材料
- 内部沟通材料
- HTML / drawio / Excel / Markdown / 飞书文档输出
- 会议推进表
- 核对清单
- 方案优劣势对比
- 多方确认事项整理

## 默认动作

1. 判断用户给的材料属于哪类工作流。
2. 如果可明确判断，直接使用对应 `jjskill-*`。
3. 如果不明确，只问 1 个关键问题。
4. 输出前确认使用场景和产物格式，除非用户已经明确指定。

## 输出格式建议

- 开会推动敲定：优先建议 Excel + HTML。
- 给领导快速看：优先建议 HTML 或 PPT。
- 跟技术同事讨论链路：优先建议 drawio。
- 沉淀正式方案：优先建议 Markdown / 飞书文档。
- 多人在线协同：优先建议飞书文档 / 飞书表格。
