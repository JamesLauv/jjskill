# jjskill

James/JJ 的个人 Agent 工作流 Skill 集合。

当前包含：

- `jjskill`：个人工作流主入口，用于判断材料整理、方案评估、会议推进等任务应该进入哪个具体工作流。
- `jjskill-doc-to-decision-artifacts`：把项目文档、技术评估、会议纪要、需求草稿等材料，通过交互共创，整理成可沟通、可决策、可推进的产物。

## 安装到 Codex

将 `skills` 目录下的 Skill 文件夹复制到 Codex skills 目录：

```powershell
Copy-Item -Recurse -Force .\skills\jjskill C:\Users\james\.codex\skills\
Copy-Item -Recurse -Force .\skills\jjskill-doc-to-decision-artifacts C:\Users\james\.codex\skills\
```

重启或开启新的 Codex 会话后，在 Available skills 中应能看到：

- `jjskill`
- `jjskill-doc-to-decision-artifacts`

## 安装到其他 Agent

如果目标 Agent 支持类似 `SKILL.md` 的本地技能目录机制，可将 `skills/<skill-name>/SKILL.md` 复制到对应目录。

如果目标 Agent 不支持 Skill 机制，可以把 `SKILL.md` 的正文作为该 Agent 的项目规则、系统提示或工作流说明使用。

## 建议使用方式

开放式材料整理时，优先触发 `jjskill`：

```text
使用 jjskill，帮我看看这份材料，整理成适合内部沟通和推进的产物。
```

明确要做“文档到决策材料”时，直接触发：

```text
使用 jjskill-doc-to-decision-artifacts，读取这份技术评估文档，先分析，再跟我交互确认输出格式。
```

## 版本维护建议

- 每次新增 Skill，用 `jjskill-xxx` 命名。
- 主入口 `jjskill` 只负责路由，不承载具体长流程。
- 具体方法论放在独立 `jjskill-*` Skill 中。
- 每次更新后，用真实工作材料测试一次触发和输出质量。
