# TalkToFigma MCP 工具使用指引

## 目錄
- [TalkToFigma MCP 工具使用指引](#talktofigma-mcp-工具使用指引)
  - [目錄](#目錄)
  - [1. 連線與初始化](#1-連線與初始化)
  - [2. 建立 Frame](#2-建立-frame)
  - [3. 建立文字](#3-建立文字)
  - [4. 建立矩形](#4-建立矩形)
  - [5. 樣式設定](#5-樣式設定)
    - [填充色](#填充色)
    - [邊框色](#邊框色)
    - [圓角](#圓角)
  - [6. 版型系統（Auto Layout）](#6-版型系統auto-layout)
    - [設定 Auto Layout](#設定-auto-layout)
    - [設定子元素尺寸行為](#設定子元素尺寸行為)
  - [7. 常用工作流程](#7-常用工作流程)
    - [建立色票卡片](#建立色票卡片)
    - [建立按鈕元件](#建立按鈕元件)
  - [8. 色彩換算](#8-色彩換算)
    - [常用顏色換算表](#常用顏色換算表)
    - [批量換算 Node.js 片段](#批量換算-nodejs-片段)

---

## 1. 連線與初始化

```
# 取得文件資訊，確認 TalkToFigma 已連線
get_document_info()

# 加入頻道（必要時）
join_channel(channel="")

# 取得目前選取的節點
get_selection()

# 取得特定節點詳情
get_node_info(nodeId="xxx")
```

**重要**：每次工作流程開始前必須先呼叫 `get_document_info()` 確認連線。

---

## 2. 建立 Frame

Frame 是 Figma 中的基本容器，等同 HTML 的 `<div>`。

```python
create_frame(
    x=0,           # 距左側距離（px）
    y=0,           # 距頂部距離（px）
    width=1440,    # 寬度（px）
    height=900,    # 高度（px）
    name="Main Frame",    # 圖層名稱
    parentId=None,        # 父節點 ID（None = 根層）
    fillColor={"r": 0.96, "g": 0.96, "b": 0.98, "a": 1},  # 背景色
    strokeColor=None,     # 邊框色（可省略）
    strokeWeight=None,    # 邊框寬度（可省略）
    # Auto Layout 相關（可省略）
    layoutMode="VERTICAL",          # NONE / HORIZONTAL / VERTICAL
    paddingTop=48,
    paddingBottom=48,
    paddingLeft=48,
    paddingRight=48,
    itemSpacing=32,                  # 子元素間距
    primaryAxisAlignItems="MIN",     # MIN / MAX / CENTER / SPACE_BETWEEN
    counterAxisAlignItems="MIN",     # MIN / MAX / CENTER
    layoutSizingHorizontal="FIXED",  # FIXED / HUG / FILL
    layoutSizingVertical="HUG"
)
```

回傳值：`{"id": "node-id", ...}` — 保存 id 供後續使用。

---

## 3. 建立文字

```python
create_text(
    x=0,
    y=0,
    text="Hello World",
    name="Title Text",          # 圖層語意名稱
    parentId="parent-node-id",  # 填入父 Frame 的 id
    fontSize=48,
    fontWeight=700,             # 400=Regular, 600=SemiBold, 700=Bold, 900=Black
    fontColor={"r": 0.08, "g": 0.08, "b": 0.12, "a": 1}
)
```

**字重對應**：
| fontWeight | CSS 等效          |
| ---------- | ----------------- |
| 100        | Thin              |
| 300        | Light             |
| 400        | Regular           |
| 500        | Medium            |
| 600        | SemiBold          |
| 700        | Bold              |
| 900        | Black / ExtraBold |

---

## 4. 建立矩形

適合用於色票、分隔線、背景色塊等：

```python
create_rectangle(
    x=0,
    y=0,
    width=200,
    height=80,
    name="Color Swatch",
    parentId="parent-node-id"
)
```

建立後再使用 `set_fill_color()` 設定顏色。

---

## 5. 樣式設定

### 填充色

```python
set_fill_color(
    nodeId="node-id",
    r=0.2,    # 0–1 範圍
    g=0.4,
    b=0.9,
    a=1       # 不透明度（1=不透明）
)
```

### 邊框色

```python
set_stroke_color(
    nodeId="node-id",
    r=0.8, g=0.8, b=0.8, a=1,
    weight=1    # 邊框寬度（px）
)
```

### 圓角

```python
set_corner_radius(
    nodeId="node-id",
    radius=8,                           # 全角
    corners=[True, True, True, True]    # [TL, TR, BR, BL] 各角個別設定
)
```

---

## 6. 版型系統（Auto Layout）

Auto Layout 讓子元素自動排列，類似 CSS Flexbox。

### 設定 Auto Layout

```python
set_layout_mode(nodeId="frame-id", layoutMode="VERTICAL")  # 或 HORIZONTAL

set_padding(
    nodeId="frame-id",
    paddingTop=24, paddingBottom=24,
    paddingLeft=24, paddingRight=24
)

set_item_spacing(nodeId="frame-id", itemSpacing=16)

set_axis_align(
    nodeId="frame-id",
    primaryAxisAlignItems="MIN",    # 主軸對齊
    counterAxisAlignItems="MIN"     # 副軸對齊
)
```

### 設定子元素尺寸行為

```python
set_layout_sizing(
    nodeId="child-id",
    layoutSizingHorizontal="FILL",  # 填滿父容器寬度
    layoutSizingVertical="HUG"      # 根據內容決定高度
)
```

---

## 7. 常用工作流程

### 建立色票卡片

```python
# 建立色票容器 Frame
swatch_frame = create_frame(
    x=0, y=0, width=160, height=200,
    name="Color Swatch - Primary",
    parentId=parent_id,
    layoutMode="VERTICAL",
    paddingTop=0, paddingBottom=16,
    paddingLeft=0, paddingRight=0,
    itemSpacing=12,
    layoutSizingHorizontal="FIXED",
    layoutSizingVertical="FIXED"
)

# 色塊矩形
color_block = create_rectangle(
    x=0, y=0, width=160, height=120,
    name="Color Block",
    parentId=swatch_frame["id"]
)
set_fill_color(nodeId=color_block["id"], r=0.18, g=0.18, b=0.98, a=1)

# 色名文字
create_text(
    x=0, y=0, text="Primary",
    name="Color Name",
    parentId=swatch_frame["id"],
    fontSize=14, fontWeight=600,
    fontColor={"r": 0.1, "g": 0.1, "b": 0.1, "a": 1}
)

# Hex code 文字
create_text(
    x=0, y=0, text="#2D2DFA",
    name="Hex Code",
    parentId=swatch_frame["id"],
    fontSize=12, fontWeight=400,
    fontColor={"r": 0.5, "g": 0.5, "b": 0.5, "a": 1}
)
```

### 建立按鈕元件

```python
btn_frame = create_frame(
    x=0, y=0, width=160, height=48,
    name="Button / Primary",
    parentId=components_section_id,
    fillColor={"r": 0.18, "g": 0.18, "b": 0.98, "a": 1},
    layoutMode="HORIZONTAL",
    paddingTop=12, paddingBottom=12,
    paddingLeft=24, paddingRight=24,
    primaryAxisAlignItems="CENTER",
    counterAxisAlignItems="CENTER",
    layoutSizingHorizontal="HUG",
    layoutSizingVertical="FIXED"
)
set_corner_radius(nodeId=btn_frame["id"], radius=8)

create_text(
    x=0, y=0, text="Button",
    name="Button Label",
    parentId=btn_frame["id"],
    fontSize=15, fontWeight=600,
    fontColor={"r": 1, "g": 1, "b": 1, "a": 1}
)
```

---

## 8. 色彩換算

Hex → Figma RGB（0–1 範圍）的換算公式：

```
r = int(hex[1:3], 16) / 255
g = int(hex[3:5], 16) / 255
b = int(hex[5:7], 16) / 255
```

### 常用顏色換算表

| Hex       | r     | g     | b     |
| --------- | ----- | ----- | ----- |
| `#FFFFFF` | 1.0   | 1.0   | 1.0   |
| `#000000` | 0.0   | 0.0   | 0.0   |
| `#F5F5F5` | 0.961 | 0.961 | 0.961 |
| `#1A1A2E` | 0.102 | 0.102 | 0.180 |
| `#E2E8F0` | 0.886 | 0.910 | 0.941 |
| `#64748B` | 0.392 | 0.455 | 0.545 |
| `#3B82F6` | 0.231 | 0.510 | 0.965 |
| `#10B981` | 0.063 | 0.725 | 0.506 |
| `#EF4444` | 0.937 | 0.267 | 0.267 |
| `#F59E0B` | 0.961 | 0.620 | 0.043 |

### 批量換算 Node.js 片段

```js
const hexToFigmaRGB = (hex) => ({
  r: parseInt(hex.slice(1, 3), 16) / 255,
  g: parseInt(hex.slice(3, 5), 16) / 255,
  b: parseInt(hex.slice(5, 7), 16) / 255,
  a: 1
})
```
