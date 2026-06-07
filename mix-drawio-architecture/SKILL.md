---
name: mix-drawio-architecture
description: 使用 draw.io 生成分层全景架构图：顶部标题栏、横向阶段/目标链路、分层泳道、左侧层级标签、模块矩阵、基础支撑层和指标层。适用于业务架构、产品架构、平台架构、能力地图、系统全景图和战略落地图。
---

# Draw.io 通用分层全景架构图技能

当用户需要把一个复杂体系整理成“全景架构图”“能力地图”“业务架构图”“组织架构图”“平台架构图”“数据架构图”“战略落地图”或类似结构化图表时，使用本技能。

本技能关注的是版式和架构表达方式，不绑定任何具体行业、业务或图片内容。生成时应根据用户提供的信息替换为真实内容；如果用户没有提供内容，使用通用占位符。

## 适用场景

- 展示一个组织、平台、产品或系统的整体能力结构。
- 将目标、参与方、核心模块、支撑底座和指标体系放在一张图中。
- 将复杂架构压缩成适合汇报、方案文档或评审使用的一页式全景图。
- 把文字清单转换为 draw.io 原生 XML 架构图。

## 视觉风格

整体风格应满足：

- 页面为横向画布，白色背景。
- 顶部使用浅色横幅承载主标题。
- 主标题居中，字号大，使用深蓝或品牌主色。
- 图中主体由多条横向分层泳道组成。
- 每一层左侧有大色块标签，右侧是该层内容。
- 每一层使用浅色背景带，层与层之间留出清晰间距。
- 重要层使用更饱和的颜色，支撑层可使用较浅的同色系背景。
- 模块卡片使用圆角矩形，边框清晰，文字居中。
- 同一层内的模块按网格或列对齐，保持严格的视觉秩序。
- 可在顶部目标链路中使用箭头连接多个目标或阶段。

## 推荐信息结构

将用户内容整理为以下通用结构：

```json
{
  "title": "架构图标题",
  "topFlow": [
    {
      "category": "阶段/方向 A",
      "node": "目标/结果 A"
    }
  ],
  "layers": [
    {
      "label": "层级名称",
      "type": "simple-row | module-grid | support-base | metric-row",
      "items": [
        {
          "title": "模块名称",
          "children": ["子项 1", "子项 2", "子项 3"]
        }
      ]
    }
  ]
}
```

字段说明：

- `title`：图表主标题。
- `topFlow`：顶部目标、阶段、流程或价值链路，可为空。
- `layers`：架构主体的横向分层。
- `label`：左侧层级标签。
- `type`：决定该层的绘制方式。
- `items`：该层中的模块、能力、系统、数据域或指标。
- `children`：模块内部子能力或子对象。

## 标准画布

默认使用横向大画布：

```text
PAGE_W = 1800
PAGE_H = 1280
MARGIN_X = 60
TITLE_X = 60
TITLE_Y = 55
TITLE_W = 1680
TITLE_H = 75

BODY_X = 60
BODY_W = 1680
LABEL_W = 280
CONTENT_X = BODY_X + LABEL_W + 20
CONTENT_W = BODY_W - LABEL_W - 40
ROW_GAP = 14
```

当内容较多时：

- 优先增加画布高度，不要压缩到文字重叠。
- 横向模块超过 5 个时，改为两行网格。
- 单个模块内子项超过 6 个时，使用两列小卡片或列表式文本。

## 分层版式

推荐从上到下组织为：

1. 标题栏
2. 顶部目标/阶段链路
3. 参与方/角色/团队/对象层
4. 核心能力/业务模块层
5. 工具/系统/应用层
6. 基础支撑/平台支撑/公共能力层
7. 指标/度量/结果层

这些层级可以按用户场景增删。不要强行保留空层。

## 配色规范

使用清晰、克制的多色体系：

```text
TITLE_BG = #dfe4ff
TITLE_TEXT = #2f4ea2

GOAL_BG = #ddf7f4
GOAL_MAIN = #36c9bd
GOAL_STROKE = #4cc9c8

ROW_BLUE_BG = #eaf4ff
ROW_BLUE_MAIN = #55a9ed
ROW_BLUE_STROKE = #49a4ff

MODULE_BG = #edf3ff
MODULE_MAIN = #4388f5
MODULE_STROKE = #4084ff

SUPPORT_BG = #f0e5fb
SUPPORT_MAIN = #7455e8
SUPPORT_CARD = #9b86e7
SUPPORT_STROKE = #785cff

METRIC_BG = #fff0f0
METRIC_MAIN = #eb5757
METRIC_STROKE = #ff4d4f

TEXT_DARK = #1f2937
TEXT_MUTED = #4b5563
WHITE = #ffffff
```

规则：

- 左侧层级标签使用该层主色，白色粗体文字。
- 右侧内容区域使用同色系浅底。
- 模块标题条使用高饱和主色，模块内容区使用浅底。
- 指标层使用红色系或强调色，表达结果导向。
- 不要只使用单一色相；至少区分目标、模块、支撑、指标四类颜色。

## Draw.io 基础形状

### 标题栏

```xml
<mxCell id="title_bg" value="" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#dfe4ff;strokeColor=none;" vertex="1" parent="1">
  <mxGeometry x="60" y="55" width="1680" height="75" as="geometry"/>
</mxCell>
<mxCell id="title_text" value="架构图标题" style="text;html=1;strokeColor=none;fillColor=none;align=center;verticalAlign=middle;whiteSpace=wrap;fontSize=40;fontStyle=1;fontColor=#2f4ea2;" vertex="1" parent="1">
  <mxGeometry x="60" y="65" width="1680" height="55" as="geometry"/>
</mxCell>
```

### 横向分层背景

```xml
<mxCell id="row_bg_1" value="" style="rounded=1;arcSize=4;whiteSpace=wrap;html=1;fillColor=#eaf4ff;strokeColor=none;" vertex="1" parent="1">
  <mxGeometry x="60" y="250" width="1680" height="95" as="geometry"/>
</mxCell>
```

### 左侧层级标签

```xml
<mxCell id="row_label_1" value="层级名称" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#55a9ed;strokeColor=none;fontColor=#ffffff;fontSize=28;fontStyle=1;align=center;verticalAlign=middle;" vertex="1" parent="1">
  <mxGeometry x="66" y="260" width="274" height="75" as="geometry"/>
</mxCell>
```

### 普通模块卡片

```xml
<mxCell id="card_1" value="模块名称" style="rounded=1;arcSize=8;whiteSpace=wrap;html=1;fillColor=#ffffff;strokeColor=#49a4ff;strokeWidth=2;fontColor=#2f80ed;fontSize=22;fontStyle=1;align=center;verticalAlign=middle;" vertex="1" parent="1">
  <mxGeometry x="370" y="265" width="255" height="58" as="geometry"/>
</mxCell>
```

### 带标题条的模块组

用于核心能力、业务模块、系统模块等需要展示子项的区域：

```xml
<mxCell id="module_header_1" value="模块名称" style="rounded=1;arcSize=4;whiteSpace=wrap;html=1;fillColor=#4388f5;strokeColor=#4084ff;fontColor=#ffffff;fontSize=22;fontStyle=1;align=center;verticalAlign=middle;" vertex="1" parent="1">
  <mxGeometry x="370" y="455" width="330" height="60" as="geometry"/>
</mxCell>
<mxCell id="module_body_1" value="子项 1&lt;br&gt;子项 2&lt;br&gt;子项 3" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#edf3ff;strokeColor=#4084ff;strokeWidth=2;fontColor=#1f2937;fontSize=20;align=center;verticalAlign=middle;lineHeight=1.7;" vertex="1" parent="1">
  <mxGeometry x="370" y="520" width="330" height="170" as="geometry"/>
</mxCell>
```

### 支撑底座容器

用于平台支撑、基础设施、公共能力、共享服务等：

```xml
<mxCell id="support_group_1" value="支撑域名称" style="rounded=1;arcSize=4;whiteSpace=wrap;html=1;fillColor=#9b86e7;strokeColor=none;fontColor=#ffffff;fontSize=22;fontStyle=1;align=center;verticalAlign=top;spacingTop=12;" vertex="1" parent="1">
  <mxGeometry x="370" y="870" width="430" height="180" as="geometry"/>
</mxCell>
```

支撑域内部可用小卡片表达子项：

```xml
<mxCell id="support_item_1" value="子能力" style="rounded=1;arcSize=6;whiteSpace=wrap;html=1;fillColor=#9b86e7;strokeColor=#ffffff;strokeWidth=2;fontColor=#ffffff;fontSize=18;align=center;verticalAlign=middle;" vertex="1" parent="1">
  <mxGeometry x="390" y="930" width="195" height="44" as="geometry"/>
</mxCell>
```

### 顶部链路箭头

用于表达目标、阶段、流程或价值传导：

```xml
<mxCell id="flow_node_1" value="目标节点" style="rounded=1;arcSize=50;whiteSpace=wrap;html=1;fillColor=#ffffff;strokeColor=#4cc9c8;strokeWidth=2;fontColor=#258a8a;fontSize=20;fontStyle=1;align=center;verticalAlign=middle;" vertex="1" parent="1">
  <mxGeometry x="360" y="190" width="245" height="58" as="geometry"/>
</mxCell>
<mxCell id="flow_arrow_1" value="" style="endArrow=block;html=1;rounded=0;strokeWidth=2;strokeColor=#258a8a;" edge="1" parent="1">
  <mxGeometry relative="1" as="geometry">
    <mxPoint x="605" y="219" as="sourcePoint"/>
    <mxPoint x="730" y="219" as="targetPoint"/>
  </mxGeometry>
</mxCell>
```

## 布局算法

1. 解析用户输入，识别标题、顶部链路、分层、模块、子项和指标。
2. 根据层级数量计算每一层高度：
   - 简单行：90-110 px。
   - 模块矩阵行：250-300 px。
   - 支撑底座行：250-320 px。
   - 指标行：90-110 px。
3. 按从上到下顺序绘制：
   - 标题栏。
   - 顶部链路或目标层。
   - 普通分层行。
   - 核心模块矩阵。
   - 支撑底座。
   - 指标层。
4. 每层先绘制浅色背景，再绘制左侧标签，最后绘制右侧内容。
5. 右侧内容区域按等宽网格分配：
   - 2 个模块：每个约占 48% 宽度。
   - 3 个模块：每个约占 31% 宽度。
   - 4 个模块：每个约占 23% 宽度。
   - 5 个模块：每个约占 18% 宽度。
6. 模块之间保持 14-20 px 间距。
7. 所有文字居中对齐，复杂说明使用 `<br>` 或 `&lt;br&gt;` 控制换行。

## XML 生成规则

- 输出 draw.io 原生 XML，扩展名使用 `.drawio`。
- 根节点使用 `<mxfile>`，内部包含一个 `<diagram>` 和 `<mxGraphModel>`。
- `mxCell` 的 id 必须唯一。
- 先绘制背景，再绘制标签和卡片，避免背景遮挡内容。
- 文本中的 `<br>` 在 XML 属性中写为 `&lt;br&gt;`。
- 中文、英文、数字混排时，控制卡片宽度，避免文字溢出。
- 除非用户要求，不使用阴影、渐变和复杂图标，保持清爽的咨询汇报风格。

## 文案规范

- 主标题：8-14 个字或一个短语，表达整张图的主题。
- 层级标签：2-8 个字，使用名词短语。
- 模块标题：2-10 个字，避免句子化。
- 子项：每项 2-8 个字，数量控制在 3-6 项。
- 指标：使用短标签，例如“指标 A”“指标 B”“结果 C”，不要写长句。
- 如用户输入过长，应先摘要再入图。

## 可选变体

### 业务能力全景图

使用层级：

```text
目标层 -> 参与方层 -> 核心能力层 -> 工具系统层 -> 基础支撑层 -> 指标层
```

### 技术平台架构图

使用层级：

```text
访问层 -> 应用层 -> 服务层 -> 数据层 -> 基础设施层 -> 监控指标层
```

### 产品路线落地图

使用层级：

```text
战略目标 -> 用户/场景 -> 产品模块 -> 运营/增长机制 -> 数据支撑 -> 结果指标
```

## 质量检查清单

交付前检查：

- 是否完全去除了示例图片中的具体业务内容。
- 标题栏、层级行、左侧标签、右侧内容是否对齐。
- 各层颜色是否有明确区分，但整体不杂乱。
- 模块卡片宽度、高度和间距是否一致。
- 文本是否全部在容器内，没有溢出或重叠。
- 复杂层是否使用模块组或子卡片，而不是堆砌长文本。
- 支撑底座是否位于主体偏下位置，形成稳定的“底座”视觉。
- 指标层是否位于底部，形成结果收束。
- draw.io XML 是否可直接打开。

## 调用提示词模板

```text
请根据以下信息生成一个 draw.io 分层全景架构图。使用顶部标题栏、横向分层泳道、左侧层级标签、右侧模块卡片、基础支撑底座和底部指标层。内容请根据输入替换，不要保留示例占位内容。
```
