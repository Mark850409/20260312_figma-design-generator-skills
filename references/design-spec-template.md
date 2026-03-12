# 設計規格文件模板

使用此模板產出 `design-spec.md`，作為 Phase 2 靜態網頁與 Phase 3 Figma 繪製的輸入規格。

---

# [專案名稱] 設計系統規格

> 版本：1.0.0 | 建立日期：[日期]

---

## 1. 設計方向 (Design Direction)

| 項目           | 說明                                             |
| -------------- | ------------------------------------------------ |
| **風格定位**   | （例：現代科技感、極簡奢華、溫暖有機、大膽前衛） |
| **目標受眾**   | （例：B2B 企業用戶、創意工作者、一般消費者）     |
| **設計關鍵字** | （3-5 個形容詞，例：精準、透明、賦能）           |
| **靈感參考**   | （可選填，例：Linear.app、Vercel、Notion）       |

---

## 2. 色彩系統 (Color System)

### 主色盤

| 角色                    | 名稱   | Hex       | RGB(0-1) | 用途                 |
| ----------------------- | ------ | --------- | -------- | -------------------- |
| `--color-primary`       | [色名] | `#XXXXXX` | r, g, b  | 主要 CTA、連結、重點 |
| `--color-primary-hover` | [色名] | `#XXXXXX` | r, g, b  | Primary 懸停狀態     |
| `--color-secondary`     | [色名] | `#XXXXXX` | r, g, b  | 次要操作、標籤       |
| `--color-accent`        | [色名] | `#XXXXXX` | r, g, b  | 強調標記、徽章       |

### 中性色盤

| 角色                     | Hex       | RGB(0-1) | 用途             |
| ------------------------ | --------- | -------- | ---------------- |
| `--color-bg`             | `#XXXXXX` | r, g, b  | 頁面背景         |
| `--color-surface`        | `#XXXXXX` | r, g, b  | 卡片/面板背景    |
| `--color-surface-2`      | `#XXXXXX` | r, g, b  | 次層面板         |
| `--color-border`         | `#XXXXXX` | r, g, b  | 邊框、分隔線     |
| `--color-text-primary`   | `#XXXXXX` | r, g, b  | 主要文字         |
| `--color-text-secondary` | `#XXXXXX` | r, g, b  | 次要文字         |
| `--color-text-muted`     | `#XXXXXX` | r, g, b  | 說明文字、佔位符 |

### 語意色

| 角色              | Hex       | RGB(0-1) | 用途     |
| ----------------- | --------- | -------- | -------- |
| `--color-success` | `#XXXXXX` | r, g, b  | 成功狀態 |
| `--color-warning` | `#XXXXXX` | r, g, b  | 警告狀態 |
| `--color-error`   | `#XXXXXX` | r, g, b  | 錯誤狀態 |
| `--color-info`    | `#XXXXXX` | r, g, b  | 資訊狀態 |

---

## 3. 字型系統 (Typography)

### 字體選擇

| 角色             | 字體名稱 | Google Fonts URL                       | 字重          |
| ---------------- | -------- | -------------------------------------- | ------------- |
| **Display Font** | [字名]   | `fonts.googleapis.com/css2?family=...` | 700, 900      |
| **Body Font**    | [字名]   | `fonts.googleapis.com/css2?family=...` | 400, 500, 600 |
| **Mono Font**    | [字名]   | `fonts.googleapis.com/css2?family=...` | 400           |

### 字型比例

| 層級       | CSS Token           | 字號 | 行高 | 字重 | 字距    | 用途       |
| ---------- | ------------------- | ---- | ---- | ---- | ------- | ---------- |
| Display XL | `--text-display-xl` | 64px | 1.1  | 900  | -0.04em | 英雄標題   |
| Display    | `--text-display`    | 48px | 1.15 | 700  | -0.03em | 頁面主標   |
| H1         | `--text-h1`         | 36px | 1.2  | 700  | -0.02em | 章節標題   |
| H2         | `--text-h2`         | 28px | 1.3  | 600  | -0.01em | 子標題     |
| H3         | `--text-h3`         | 22px | 1.35 | 600  | 0       | 卡片標題   |
| Body L     | `--text-body-l`     | 18px | 1.6  | 400  | 0       | 主段落     |
| Body       | `--text-body`       | 16px | 1.6  | 400  | 0       | 預設正文   |
| Body S     | `--text-body-s`     | 14px | 1.5  | 400  | 0       | 輔助文字   |
| Caption    | `--text-caption`    | 12px | 1.4  | 500  | 0.02em  | 標籤、說明 |

---

## 4. 間距系統 (Spacing)

```
--space-1:   4px
--space-2:   8px
--space-3:  12px
--space-4:  16px
--space-5:  20px
--space-6:  24px
--space-8:  32px
--space-10: 40px
--space-12: 48px
--space-16: 64px
--space-20: 80px
--space-24: 96px
```

---

## 5. 圓角 (Border Radius)

```
--radius-none: 0px
--radius-sm:   4px
--radius-md:   8px
--radius-lg:  12px
--radius-xl:  16px
--radius-2xl: 24px
--radius-full: 9999px
```

---

## 6. 陰影 (Shadows)

```css
--shadow-sm:  0 1px 3px rgba(0,0,0,0.08), 0 1px 2px rgba(0,0,0,0.06);
--shadow-md:  0 4px 12px rgba(0,0,0,0.10), 0 2px 6px rgba(0,0,0,0.08);
--shadow-lg:  0 10px 30px rgba(0,0,0,0.12), 0 4px 12px rgba(0,0,0,0.08);
--shadow-xl:  0 20px 60px rgba(0,0,0,0.15), 0 8px 20px rgba(0,0,0,0.10);
```

---

## 7. 元件規格 (Components)

### Button

| 變體      | 背景色      | 文字色         | Border       | 圓角 | 內距      | 字號/字重  |
| --------- | ----------- | -------------- | ------------ | ---- | --------- | ---------- |
| Primary   | `primary`   | white          | none         | `md` | 12px 24px | 15px / 600 |
| Secondary | `surface`   | `primary`      | 1px `border` | `md` | 12px 24px | 15px / 600 |
| Ghost     | transparent | `text-primary` | none         | `md` | 12px 24px | 15px / 500 |
| Danger    | `error`     | white          | none         | `md` | 12px 24px | 15px / 600 |

### Card

| 屬性 | 值                   |
| ---- | -------------------- |
| 背景 | `--color-surface`    |
| 邊框 | 1px `--color-border` |
| 圓角 | `--radius-xl` (16px) |
| 陰影 | `--shadow-md`        |
| 內距 | `--space-6` (24px)   |

### Input

| 屬性       | 值                    |
| ---------- | --------------------- |
| 背景       | `--color-bg`          |
| 邊框       | 1px `--color-border`  |
| 圓角       | `--radius-md` (8px)   |
| 內距       | 10px 16px             |
| 字號       | 15px / Regular        |
| Focus 邊框 | 2px `--color-primary` |

### Badge / Tag

| 變體    | 背景          | 文字             | 圓角   | 內距     |
| ------- | ------------- | ---------------- | ------ | -------- |
| Default | `surface-2`   | `text-secondary` | `full` | 4px 10px |
| Primary | `primary` 15% | `primary`        | `full` | 4px 10px |
| Success | `success` 15% | `success`        | `full` | 4px 10px |

---

## 8. Figma 繪製摘要 (Figma Render Summary)

> 此區塊供 AI Agent 在 Phase 3 時快速參照。

### 頁面結構

```
Main Frame (1440 × auto)
├── Header Section
│   ├── 標題 Frame
│   └── 說明文字
├── Color System Section
│   └── Color Grid (wrap)
│       └── Color Swatch Card × N
├── Typography Section
│   └── Type Scale Frame (vertical)
│       └── Type Row × N
├── Spacing Section
│   └── Spacing Row × N
└── Components Section
    ├── Button Group Frame
    ├── Card Demo Frame
    └── Input Demo Frame
```

### 色票卡片規格

- 外框 Frame：160 × 200px，VERTICAL Auto Layout，padding 0 0 16 0，gap 12
- 色塊矩形：160 × 120px
- 色名文字：14px / 600
- Hex Code 文字：12px / 400 / text-muted

### 字型展示行規格

- 單行 Frame：HORIZONTAL Auto Layout，FILL 寬度，HUG 高度，padding 16 0，gap 16
- 左側標籤：80px 固定寬，12px / 500 / muted
- 右側樣本文字：對應字號/字重
