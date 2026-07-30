# 输出格式规格说明

本文档定义了多源资料逻辑重构的各输出格式规格。生成产物时参照对应章节。

---

## 1. DrawIO

用于流程讨论和技术对齐。可用 diagrams.net 打开编辑。

### 结构规范

```xml
<mxfile>
  <diagram>
    <mxGraphModel>
      <root>
        <!-- 标题 -->
        <!-- 泳道/分组 (swimlane) -->
        <!-- 节点 (vertex) -->
        <!-- 连线 (edge) -->
        <!-- 图例 -->
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

### 节点颜色编码

| 颜色 | 用途 | fill stroke 示例 |
|---|---|---|
| 橙色系 | 直营客户退货原因大类 | `#FFCC80` / `#F57C00` |
| 绿色系 | 非直营客户退货原因大类 | `#C8E6C9` / `#388E3C` |
| 黄色系 | 场景细分/条件 | `#FFF9C4` / `#F9A825` |
| 蓝色系 | 对应处理方式 | `#E3F2FD` / `#1976D2` |
| 紫色虚线 | 二期优化/系统处理 | `#F3E5F5` / `#7B1FA2` dashed |
| 红色虚线 | 特殊约束/例外 | `#FFEBEE` / `#D32F2F` |

### 布局规则

- 标题居中，字号 22px，加粗
- 泳道（swimlane）包裹同一大类的所有节点
- 节点宽度 120-200px，高度 25-35px
- 连线使用 orthogonalEdgeStyle，圆角
- 底部图例区，背景浅灰，包含所有颜色含义
- 特殊说明（如"仅适用于XX"）用红色斜体标注在图例区

### XML 模板

标题：
```xml
<mxCell id="title" value="标题文字" style="text;html=1;fontSize=22;fontStyle=1;align=center;" vertex="1" parent="1">
  <mxGeometry x="550" y="20" width="500" height="40" as="geometry"/>
</mxCell>
```

泳道：
```xml
<mxCell id="group_id" value="分组名称" style="swimlane;startSize=30;fillColor=#FFF3E0;strokeColor=#FF9800;fontStyle=1;fontSize=13;rounded=1;" vertex="1" parent="1">
  <mxGeometry x="30" y="80" width="520" height="580" as="geometry"/>
</mxCell>
```

普通节点：
```xml
<mxCell id="node_id" value="节点文字" style="rounded=1;fillColor=#FFF9C4;strokeColor=#F9A825;fontSize=10;whiteSpace=wrap;" vertex="1" parent="group_id">
  <mxGeometry x="170" y="40" width="120" height="25" as="geometry"/>
</mxCell>
```

连线：
```xml
<mxCell id="edge_id" style="edgeStyle=orthogonalEdgeStyle;rounded=1;strokeColor=#4CAF50;strokeWidth=1.5;" edge="1" source="source_id" target="target_id" parent="group_id">
  <mxGeometry relative="1" as="geometry"/>
</mxCell>
```

---

## 2. SVG

用于正式文档嵌入和矢量输出。自包含，不依赖外部资源。

### 结构规范

```xml
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 宽度 高度" font-family="Microsoft YaHei, PingFang SC, sans-serif">
  <defs>
    <filter id="shadow">...</filter>
  </defs>
  <!-- 背景 -->
  <!-- 标题区 -->
  <!-- 内容区（通常左右分栏） -->
  <!-- 图例区 -->
</svg>
```

### 颜色编码

与 DrawIO 保持一致。使用内联 `fill` 和 `stroke` 属性。

### 布局规则

- viewBox 宽度建议 1400px，高度按内容自适应
- 背景色 `#F5F5F5`，圆角 `rx="8"`
- 标题区：渐变背景矩形 + 白色文字
- 分栏区：白色卡片 + 圆角 + 投影（filter）
- 分栏标题栏：实色背景 + 白色文字
- 节点使用 `<rect>` + `<text>` 组合
- 连线使用 `<line>` 或 `<path>`
- 图例区：白色卡片，横向排列

---

## 3. HTML

用于汇报浏览和快速查看。单文件交互式页面。

### 技术规格

- 单文件 HTML
- Tailwind CSS CDN: `<script src="https://cdn.tailwindcss.com"></script>`
- 原生 JavaScript（Tab 切换等交互）
- 不使用 React / npm / 构建工具
- 浏览器直接打开

### 页面结构

```
┌─────────────────────────────────┐
│          标题区                   │
├────────────────┬────────────────┤
│   左栏（分类A）  │   右栏（分类B）  │
│  ┌──────────┐  │  ┌──────────┐  │
│  │  场景1    │  │  │  场景1    │  │
│  │  → 处理   │  │  │  → 处理   │  │
│  └──────────┘  │  └──────────┘  │
│  ┌──────────┐  │  ┌──────────┐  │
│  │  场景2    │  │  │  场景2    │  │
│  │  → 处理   │  │  │  → 处理   │  │
│  └──────────┘  │  └──────────┘  │
├────────────────┴────────────────┤
│          图例区                   │
├─────────────────────────────────┤
│          特殊说明区               │
└─────────────────────────────────┘
```

### 颜色编码

与 DrawIO 保持一致，使用 Tailwind 类名或内联样式：

| 用途 | 背景 | 边框 | 文字 |
|---|---|---|---|
| 原因大类 | `#FFF3E0` / `#E8F5E9` | `#FF9800` / `#4CAF50` | 加粗 |
| 场景细分 | `#FFFDE7` | `#FFF176` | `#5D4037` |
| 处理方式 | `#E3F2FD` | `#90CAF9` | `#1565C0` |
| 系统处理 | `#F3E5F5` | `#CE93D8` dashed | `#6A1B9A` |
| 最终结果 | `#E8F5E9` | `#A5D6A7` | `#2E7D32` 加粗 |

### 交互要求

- 场景卡片 hover 时背景变 `#fafafa`
- 流程节点间用 SVG 箭头连接
- 响应式布局：`@media (max-width: 900px)` 切换为单列

---

## 4. Excel

用于数据化管理、会上使用、筛选排序。

### Sheet 结构

典型多 Sheet 结构：

| Sheet | 用途 | 必需 |
|---|---|---|
| 总览 | 全量数据，支持筛选 | 是 |
| 分类视图A | 按第一个维度分类 | 可选 |
| 分类视图B | 按第二个维度分类 | 可选 |
| 对比视图 | 维度间差异对比 | 可选 |
| 规则补充 | 补充约束和规则 | 可选 |

### 样式规范

表头：
- 字体：微软雅黑，10pt，加粗，白色
- 背景：深色（如 `#283593`、`#FF9800`、`#4CAF50`）
- 对齐：居中
- 高度：28px

数据行：
- 字体：微软雅黑，10pt，`#333333`
- 对齐：左对齐，自动换行
- 边框：细线，`#BDBDBD`
- 行高：30-50px（按内容）

特殊列：
- 处理方式列：浅蓝背景 `#E3F2FD`
- 分类列：对应颜色浅底（如橙色 `#FFF3E0`、绿色 `#E8F5E9`）
- 备注/约束列：红色小字 `#D32F2F`，9pt

### 必需功能

- 表头冻结（freeze_panes）
- 自动筛选（auto_filter）
- 合并同类单元格（减少视觉噪音）
- 列宽自适应内容

### 生成方式

优先使用 `scripts/gen_excel.py` 脚本，传入 JSON 配置生成。

如果需要更复杂的样式（如条件格式、数据验证），可以内联生成 Python 代码执行。

---

## 颜色一致性

所有格式使用统一的颜色编码体系：

| 类别 | 主色 | 浅色 |
|---|---|---|
| 直营客户 | `#FF9800` | `#FFF3E0` |
| 非直营客户 | `#4CAF50` | `#E8F5E9` |
| 场景细分 | `#F9A825` | `#FFFDE7` |
| 处理方式 | `#1976D2` | `#E3F2FD` |
| 系统/二期 | `#7B1FA2` | `#F3E5F5` |
| 结果 | `#2E7D32` | `#E8F5E9` |
| 强调/例外 | `#D32F2F` | `#FFEBEE` |

保持颜色一致的好处：用户在不同格式间切换时，颜色含义不需要重新学习。
