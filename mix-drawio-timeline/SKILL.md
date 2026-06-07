---
name: mix-drawio-timeline
description: 使用 draw.io 生成通用横向箭头时间轴：彩色 step 箭头主轴、上下交替的信息块、垂直连接线和圆点标记。适用于历史脉络、产品路线图、项目里程碑、战略规划、活动排期和任意按时间顺序组织的信息。
---

# Draw.io 通用横向箭头时间轴技能

当用户要求把时间轴图片、时间顺序清单、历史脉络、产品路线图、项目计划、阶段节点或任何按时间排序的信息整理成 draw.io 图表时，使用本技能。目标视觉风格是一条由多个彩色箭头段拼接而成的横向主轴，每个节点位于一个箭头段中心，节点说明在主轴上方和下方交替排布。

## 视觉模式

图表应符合以下结构：

- 页面中部是一条横向时间轴主线。
- 每个时间节点对应一个箭头形色块，通常使用 `shape=step`。
- 相邻色块之间用白色描边形成分隔。
- 色块内显示日期或年份，使用白色粗体文字。
- 节点标题和说明位于主轴外侧，通过细竖线和小圆点连接到对应色块。
- 节点说明上下交替：
  - 第 1、3、5 个节点放在主轴上方。
  - 第 2、4、6 个节点放在主轴下方。
- 标题使用深色粗体，字号大于说明文字。
- 说明文字使用偏灰蓝色，行宽较短，便于阅读。
- 色彩从左到右由冷色蓝、紫逐渐过渡到粉、红。

## 输入数据

每个节点至少包含：

```json
{
  "date": "YYYY / 阶段 / 时间范围",
  "title": "节点标题",
  "description": "用 1-2 句话概括该节点的背景、动作、结果或意义。"
}
```

推荐节点数量为 3-8 个。超过 8 个节点时，应缩小箭头段宽度和字号，或拆成多行时间轴。

## 版式参数

6 个节点的默认参数：

```text
PAGE_W = 1740
PAGE_H = 720
LEFT = 40
AXIS_Y = 338
SEG_W = 285
SEG_H = 44
SEG_GAP = 0
EVENT_CENTER_X = LEFT + i * SEG_W + SEG_W / 2

DOT_SIZE = 10
DOT_ABOVE_Y = AXIS_Y - 46
DOT_BELOW_Y = AXIS_Y + SEG_H + 37
LINE_ABOVE_Y1 = DOT_ABOVE_Y + DOT_SIZE
LINE_ABOVE_Y2 = AXIS_Y
LINE_BELOW_Y1 = AXIS_Y + SEG_H
LINE_BELOW_Y2 = DOT_BELOW_Y

TEXT_W = 245
TITLE_H = 36
DESC_H = 120
TITLE_ABOVE_Y = 92
DESC_ABOVE_Y = 150
TITLE_BELOW_Y = 444
DESC_BELOW_Y = 500
```

按节点数量缩放页面宽度：

```text
PAGE_W = max(1200, LEFT * 2 + N * SEG_W)
SEG_W = min(285, floor((PAGE_W - LEFT * 2) / N))
```

## Draw.io 形状规则

### 时间轴箭头段

每个节点使用一个 `mxCell`：

```xml
<mxCell id="seg_1" value="YYYY" style="shape=step;whiteSpace=wrap;html=1;fixedSize=1;fillColor=#4f79bd;strokeColor=#ffffff;strokeWidth=6;fontColor=#ffffff;fontSize=22;fontStyle=1;align=center;verticalAlign=middle;" vertex="1" parent="1">
  <mxGeometry x="40" y="338" width="285" height="44" as="geometry"/>
</mxCell>
```

要点：

- 使用 `shape=step` 生成箭头段。
- 使用 `strokeColor=#ffffff` 和 `strokeWidth=6` 形成相邻箭头段之间的白色分隔。
- 日期文字居中、加粗、白色。
- 最后一个节点仍可使用 `shape=step`，让时间轴以箭头形态收尾。

### 圆点标记

```xml
<mxCell id="dot_1" value="" style="ellipse;whiteSpace=wrap;html=1;aspect=fixed;fillColor=#4f79bd;strokeColor=none;" vertex="1" parent="1">
  <mxGeometry x="177" y="292" width="10" height="10" as="geometry"/>
</mxCell>
```

圆点颜色应与对应箭头段颜色一致。

### 垂直连接线

```xml
<mxCell id="line_1" value="" style="endArrow=none;html=1;rounded=0;strokeWidth=3;strokeColor=#4f79bd;" edge="1" parent="1">
  <mxGeometry width="50" height="50" relative="1" as="geometry">
    <mxPoint x="182" y="302" as="sourcePoint"/>
    <mxPoint x="182" y="338" as="targetPoint"/>
  </mxGeometry>
</mxCell>
```

垂直连接线不要使用箭头。

### 节点标题

```xml
<mxCell id="title_1" value="节点标题" style="text;html=1;strokeColor=none;fillColor=none;align=center;verticalAlign=middle;whiteSpace=wrap;rounded=0;fontSize=28;fontStyle=1;fontColor=#202832;" vertex="1" parent="1">
  <mxGeometry x="60" y="104" width="245" height="36" as="geometry"/>
</mxCell>
```

标题应居中放置，并与对应箭头段的中心线对齐。

### 节点说明

```xml
<mxCell id="desc_1" value="用简短文字概括该节点的&lt;br&gt;关键动作、结果或意义。" style="text;html=1;strokeColor=none;fillColor=none;align=center;verticalAlign=top;whiteSpace=wrap;rounded=0;fontSize=22;fontStyle=1;fontColor=#718399;spacingTop=4;lineHeight=1.45;" vertex="1" parent="1">
  <mxGeometry x="60" y="154" width="245" height="130" as="geometry"/>
</mxCell>
```

说明文字应简洁。中文内容如果需要精确控制换行，可手动插入 `&lt;br&gt;`。

## 配色方案

节点颜色使用紫蓝幻粉的递进颜色，比如：

```text
1 #4f79bd 蓝色
2 #6254a3 靛紫
3 #8d50aa 紫色
4 #d34b9f 洋红
5 #ed1679 粉红
6 #fb4140 红色
```

其他节点数量可在蓝色到红色之间插值，或选择相邻且对比清晰的颜色。圆点和连接线使用对应箭头段的颜色。

## 生成流程

1. 将用户提供的节点整理为 `date`、`title`、`description` 三个字段。
2. 根据节点数量 `N` 计算页面宽度、箭头段宽度和每个节点的中心点。
3. 先从左到右绘制时间轴箭头主轴。
4. 逐个绘制节点：
   - 计算 `centerX`。
   - 奇数序号节点放在主轴上方。
   - 偶数序号节点放在主轴下方。
   - 圆点和连接线使用当前节点的箭头段颜色。
   - 标题位于说明文字上方。
5. 所有标题和说明文本框都以对应箭头段中心线居中。
6. 输出完整 `.drawio` XML 文件，根节点使用 `mxfile`，内部包含一个 `diagram`。

## 文字规范

- 日期标签：18-24 px，白色，粗体。
- 节点标题：24-30 px，深色中性文字，粗体。
- 节点说明：18-22 px，灰蓝色，中等或半粗字重。
- 每段说明控制在 3-5 行视觉文本。
- 中文内容使用全角标点。
- 避免长段落，优先做概括性摘要。

## 质量检查清单

交付 draw.io 文件前检查：

- 箭头主轴水平对齐，视觉上连续。
- 每个箭头段之间的白色分隔一致。
- 每个日期都在对应箭头段中居中。
- 每条连接线落在对应箭头段中心。
- 圆点与连接线对齐。
- 上方和下方节点块按顺序交替。
- 文本框不与主轴或相邻节点重叠。
- 页面上下左右留白足够。
- 色彩递进清晰，不被单一色相主导。
- 每次画完，检查文件是否正确，防止出错。

## 示例提示词

```text
请为以下时间节点创建一个 draw.io 横向箭头时间轴。使用上下交替的节点说明、从蓝到红的彩色 step 箭头段、圆点标记和垂直连接线。
```
