# HTML/CSS 元素 → Figma MCP 對應表

## 目錄
1. [基本容器對應](#1-基本容器對應)
2. [文字元素對應](#2-文字元素對應)
3. [視覺元素對應](#3-視覺元素對應)
4. [CSS Flexbox → Auto Layout](#4-css-flexbox--auto-layout)
5. [常見 CSS 屬性對應](#5-常見-css-屬性對應)

---

## 1. 基本容器對應

| HTML/CSS                         | Figma 元素           | MCP 工具                                  |
| -------------------------------- | -------------------- | ----------------------------------------- |
| `<div>` / `<section>` / `<main>` | Frame                | `create_frame()`                          |
| `<div>` 背景色方塊               | Frame with fillColor | `create_frame(fillColor=...)`             |
| 純色背景 `<div>`                 | Rectangle            | `create_rectangle()` + `set_fill_color()` |
| `<img>`                          | Rectangle (佔位)     | `create_rectangle()`                      |
| 分隔線 `<hr>`                    | Rectangle (高度=1)   | `create_rectangle(height=1)`              |

---

## 2. 文字元素對應

| HTML 元素          | Figma 用途 | fontSize | fontWeight |
| ------------------ | ---------- | -------- | ---------- |
| `<h1>` Display     | 英雄標題   | 48–64    | 700–900    |
| `<h1>`             | 頁面主標   | 36–48    | 700        |
| `<h2>`             | 章節標題   | 28–36    | 600–700    |
| `<h3>`             | 子標題     | 22–28    | 600        |
| `<h4>`, `<h5>`     | 小標       | 16–20    | 600        |
| `<p>` 主段落       | 正文       | 16–18    | 400        |
| `<p>` 輔助文字     | 小字       | 13–14    | 400        |
| `<label>`          | 表單標籤   | 14       | 500        |
| `<code>`, `<pre>`  | Mono 文字  | 13–14    | 400        |
| `<span>` 標籤/徽章 | 小型文字   | 11–12    | 500–600    |

**注意**：Figma 的 `create_text()` 不接受 fontFamily 參數。字體必須在 Figma 端已安裝，或使用 Figma 預設字體（如 Inter）。

---

## 3. 視覺元素對應

### CSS Box Model → Figma Frame

```
CSS:
  background-color → fillColor
  border           → set_stroke_color() + set_corner_radius()
  border-radius    → set_corner_radius(radius=N)
  box-shadow       → 僅支援視覺參考，TalkToFigma 無直接 API
  opacity          → fillColor.a（填充透明度）
```

### CSS Grid/Flexbox → Auto Layout

```
display: flex; flex-direction: column → layoutMode="VERTICAL"
display: flex; flex-direction: row    → layoutMode="HORIZONTAL"
flex-wrap: wrap                       → layoutWrap="WRAP"
gap: 16px                             → itemSpacing=16
padding: 24px                         → paddingTop/Bottom/Left/Right=24
justify-content: flex-start           → primaryAxisAlignItems="MIN"
justify-content: flex-end             → primaryAxisAlignItems="MAX"
justify-content: center               → primaryAxisAlignItems="CENTER"
justify-content: space-between        → primaryAxisAlignItems="SPACE_BETWEEN"
align-items: flex-start               → counterAxisAlignItems="MIN"
align-items: center                   → counterAxisAlignItems="CENTER"
align-items: flex-end                 → counterAxisAlignItems="MAX"
```

### CSS 尺寸 → Figma 尺寸模式

```
width: 200px (固定)    → layoutSizingHorizontal="FIXED", width=200
width: 100%            → layoutSizingHorizontal="FILL"
width: fit-content     → layoutSizingHorizontal="HUG"
height: 48px (固定)    → layoutSizingVertical="FIXED", height=48
height: auto           → layoutSizingVertical="HUG"
```

---

## 4. CSS Flexbox → Auto Layout

### 對應範例

**HTML/CSS**:
```html
<div style="display:flex; flex-direction:row; gap:16px; padding:24px; align-items:center;">
  <button>Click</button>
  <span>Label</span>
</div>
```

**Figma MCP**:
```python
container = create_frame(
    x=0, y=0, width=400, height=72,
    layoutMode="HORIZONTAL",
    itemSpacing=16,
    paddingTop=24, paddingBottom=24,
    paddingLeft=24, paddingRight=24,
    counterAxisAlignItems="CENTER",
    layoutSizingHorizontal="FIXED",
    layoutSizingVertical="HUG"
)
```

---

## 5. 常見 CSS 屬性對應

| CSS 屬性                    | Figma MCP 等效                                               |
| --------------------------- | ------------------------------------------------------------ |
| `background: #3B82F6`       | `set_fill_color(r=0.231, g=0.510, b=0.965, a=1)`             |
| `background: transparent`   | `set_fill_color(r=0, g=0, b=0, a=0)`                         |
| `border: 1px solid #E2E8F0` | `set_stroke_color(r=0.886, g=0.910, b=0.941, a=1, weight=1)` |
| `border-radius: 8px`        | `set_corner_radius(radius=8)`                                |
| `border-radius: 50%`        | `set_corner_radius(radius=9999)`                             |
| `font-size: 16px`           | `fontSize=16` (in create_text)                               |
| `font-weight: 600`          | `fontWeight=600` (in create_text)                            |
| `color: #1E293B`            | `fontColor={"r":0.118,"g":0.161,"b":0.231,"a":1}`            |
| `opacity: 0.5`              | `a=0.5` in fillColor 或 fontColor                            |
| `width: 100%; height: 48px` | `layoutSizingHorizontal="FILL", height=48`                   |

---

## 6. 設計規格頁面標準佈局

### 整體 Frame 結構

```
DesignSpec Page (1440 × HUG, VERTICAL, padding 80px)
├── page-header (VERTICAL, gap 12)
│   ├── 主標題 (Display, 48px, 700)
│   └── 副標題 (body, 18px, 400, text-secondary)
│
├── section: Color System (VERTICAL, gap 32)
│   ├── section-title ("Color System", H2 28px 600)
│   └── color-grid (HORIZONTAL, WRAP, gap 20)
│       └── color-swatch-card × n (160 × 200px)
│
├── section: Typography (VERTICAL, gap 24)
│   ├── section-title ("Typography", H2)
│   └── type-scale-list (VERTICAL, gap 0)
│       └── type-row × n (HORIZONTAL, FILL, padding 20 0)
│
├── section: Spacing (VERTICAL, gap 24)
│   ├── section-title ("Spacing", H2)
│   └── spacing-demo-list (VERTICAL, gap 12)
│       └── spacing-row × n
│
└── section: Components (VERTICAL, gap 32)
    ├── section-title ("Components", H2)
    ├── subsection: Buttons (HORIZONTAL, WRAP, gap 12)
    │   └── button-frame × n
    ├── subsection: Cards
    └── subsection: Inputs
```

### 建立建議

1. **由外而內**：先建立父 Frame，取得 id，再建立子元素。
2. **保存所有 id**：每個 `create_frame()` / `create_rectangle()` / `create_text()` 都要保存回傳的 id。
3. **高保真度間距**：觀察原圖，側邊欄寬度、卡片間距、文字邊距必須精確設定。
4. **圖標替代方案**：
   - 使用 Unicode (如 🔔, ✉️, ⚙️, 📊, ➕)。
   - 使用 `create_rectangle()` 建立小色塊組合作為簡約圖標。
5. **Auto Layout 優先**：所有容器必須設定 `layoutMode` 及其對齊方式，確保縮放邏輯正確。
6. **細節補完**：圖表中的坐標軸文字、導航欄中的微小紅點通知等必須全數繪製。
