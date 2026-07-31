# jjskill

James/JJ 的个人 Agent 工作流 Skill 集合。

当前包含：

- `jjskill`：个人工作流主入口，用于判断材料整理、方案评估、会议推进等任务应该进入哪个具体工作流。
- `jjskill-doc-to-decision-artifacts`：把项目文档、技术评估、会议纪要、需求草稿等材料，通过交互共创，整理成可沟通、可决策、可推进的产物。
- `jjskill-demo-test-framework`：分析客户业务文档，生成智能客服/对话式AI产品的Demo测试框架（测试脚本、流程图、WEB对话模拟、用例跟踪表）。
- `jjskill-multi-source-restructure`：把多份多格式资料（图片、PPT、Word、Excel等），提取内容、融合去重、建立统一逻辑框架，输出为结构化的多格式产物（drawio/svg/html/xlsx）。

## 安装方式

### 方式 1：通过 skills CLI 安装

如果你的 Agent 环境支持 `skills` CLI，可直接安装整个仓库：

```bash
npx -y skills https://github.com/JamesLauv/jjskill -g --all
```

### 方式 2：直接让 Agent 安装

把下面这句话发给支持安装 Skill 的 Agent：

```text
安装这个 skill，GitHub 地址：https://github.com/JamesLauv/jjskill
```

Agent 会根据自身的 Skill / Workflow / Rule 机制读取并安装仓库中的 Skill。

## 仓库结构

```text
skills/
  jjskill/
    SKILL.md

  jjskill-doc-to-decision-artifacts/
    SKILL.md

  jjskill-demo-test-framework/
    SKILL.md

  jjskill-multi-source-restructure/
    SKILL.md
    scripts/
      extract_pptx.py
      extract_docx.py
      gen_excel.py
    references/
      output_formats.md
```

## 路由关系

```text
jjskill (主入口)
├── jjskill-doc-to-decision-artifacts    单文档 → 决策材料
├── jjskill-demo-test-framework         客户文档 → Demo测试框架
└── jjskill-multi-source-restructure    多源 → 逻辑重构
```

路由判断：
- 1份文档 + 做决策 → `jjskill-doc-to-decision-artifacts`
- 客户业务文档 + Demo测试/测试脚本/对话模拟/流程图标注 → `jjskill-demo-test-framework`
- 多份/多格式资料 + 整理逻辑 → `jjskill-multi-source-restructure`
- 图片截图要整理 → `jjskill-multi-source-restructure`

## 建议使用方式

开放式材料整理时，优先触发 `jjskill`：

```text
使用 jjskill，帮我看看这份材料，整理成适合内部沟通和推进的产物。
```

明确要做"文档到决策材料"时，直接触发：

```text
使用 jjskill-doc-to-decision-artifacts，读取这份技术评估文档，先分析，再跟我交互确认输出格式。
```

有多份资料需要整理逻辑时，直接触发：

```text
使用 jjskill-multi-source-restructure，把这几份截图和PPT整理成流程图。
```

需要做智能客服Demo测试时，直接触发：

```text
使用 jjskill-demo-test-framework，分析这个客户的售后流程文档，生成测试脚本和对话模拟。
```

## 版本维护建议

- 每次新增 Skill，用 `jjskill-xxx` 命名。
- 主入口 `jjskill` 只负责路由，不承载具体长流程。
- 具体方法论放在独立 `jjskill-*` Skill 中。
- 每次更新后，用真实工作材料测试一次触发和输出质量。
