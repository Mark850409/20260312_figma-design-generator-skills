# NovaPulse 設計系統規格（範例）

> 版本：1.0.0 | 建立日期：2026-03-12
> 風格：現代科技感，帶有溫暖的生命力

---

## 1. 設計方向

| 項目           | 說明                                       |
| -------------- | ------------------------------------------ |
| **風格定位**   | 現代科技，溫有機感——精準、動態、充滿生命力 |
| **目標受眾**   | SaaS 產品的 B2B 用戶，重視效率與美感       |
| **設計關鍵字** | 清晰 / 賦能 / 流動 / 精準                  |
| **靈感參考**   | Linear.app、Vercel Dashboard、Raycast      |

---

## 2. 色彩系統

### 主色盤

| 角色                    | 名稱           | Hex       | RGB(0-1)            | 用途       |
| ----------------------- | -------------- | --------- | ------------------- | ---------- |
| `--color-primary`       | Nova Blue      | `#2563EB` | 0.145, 0.388, 0.922 | CTA、連結  |
| `--color-primary-hover` | Nova Blue Dark | `#1D4ED8` | 0.114, 0.306, 0.847 | Hover 狀態 |
| `--color-secondary`     | Slate          | `#475569` | 0.278, 0.333, 0.412 | 次要操作   |
| `--color-accent`        | Pulse Amber    | `#F59E0B` | 0.961, 0.620, 0.043 | 強調、通知 |

### 中性色盤

| 角色                     | Hex       | RGB(0-1)            | 用途     |
| ------------------------ | --------- | ------------------- | -------- |
| `--color-bg`             | `#F8FAFC` | 0.973, 0.980, 0.988 | 頁面背景 |
| `--color-surface`        | `#FFFFFF` | 1, 1, 1             | 卡片背景 |
| `--color-surface-2`      | `#F1F5F9` | 0.945, 0.961, 0.976 | 次層面板 |
| `--color-border`         | `#E2E8F0` | 0.886, 0.910, 0.941 | 邊框線   |
| `--color-text-primary`   | `#0F172A` | 0.059, 0.090, 0.165 | 主標題   |
| `--color-text-secondary` | `#1E293B` | 0.118, 0.161, 0.231 | 正文     |
| `--color-text-muted`     | `#64748B` | 0.392, 0.455, 0.545 | 說明文字 |

### 語意色

| 角色              | Hex       | RGB(0-1)            |
| ----------------- | --------- | ------------------- |
| `--color-success` | `#10B981` | 0.063, 0.725, 0.506 |
| `--color-warning` | `#F59E0B` | 0.961, 0.620, 0.043 |
| `--color-error`   | `#EF4444` | 0.937, 0.267, 0.267 |
| `--color-info`    | `#3B82F6` | 0.231, 0.510, 0.965 |

---

## 3. 字型系統

### 字體選擇

| 角色        | 字體           | Google Fonts                      |
| ----------- | -------------- | --------------------------------- |
| **Display** | Syne           | `family=Syne:wght@700;800`        |
| **Body**    | DM Sans        | `family=DM+Sans:wght@400;500;600` |
| **Mono**    | JetBrains Mono | `family=JetBrains+Mono:wght@400`  |

### 字型比例

| 層級       | 字號 | 字重 | 字距    | 行高 |
| ---------- | ---- | ---- | ------- | ---- |
| Display XL | 64px | 800  | -0.04em | 1.1  |
| Display    | 48px | 700  | -0.03em | 1.15 |
| H1         | 36px | 700  | -0.02em | 1.2  |
| H2         | 28px | 600  | -0.01em | 1.3  |
| H3         | 22px | 600  | 0       | 1.35 |
| Body L     | 18px | 400  | 0       | 1.6  |
| Body       | 16px | 400  | 0       | 1.6  |
| Body S     | 14px | 400  | 0       | 1.5  |
| Caption    | 12px | 500  | 0.02em  | 1.4  |

---

## 4. 元件規格

### Button

| 變體      | 背景        | 文字      | 圓角 | 內距      |
| --------- | ----------- | --------- | ---- | --------- |
| Primary   | `#2563EB`   | White     | 8px  | 12px 24px |
| Secondary | `#F1F5F9`   | `#1E293B` | 8px  | 12px 24px |
| Ghost     | transparent | `#0F172A` | 8px  | 12px 24px |
| Danger    | `#EF4444`   | White     | 8px  | 12px 24px |

### Card

- 背景：`#FFFFFF`
- 邊框：1px `#E2E8F0`
- 圓角：16px
- 陰影：`0 4px 12px rgba(0,0,0,0.10)`
- 內距：24px

### Input

- 背景：`#F8FAFC`
- 邊框：1px `#E2E8F0`，Focus 時 2px `#2563EB`
- 圓角：8px
- 內距：10px 16px
- 字號：15px / Regular

---

## 5. Figma 繪製摘要

### 頁面結構

```
NovaPulse Design Spec (1440 × HUG, VERTICAL, padding 80)
├── Header (VERTICAL, gap 12)
│   ├── "NovaPulse Design System" (64px, 800, #0F172A)
│   └── "版本 1.0.0 · 2026-03-12" (16px, 400, #64748B)
├── Color System (VERTICAL, gap 32)
│   └── color-grid (HORIZONTAL, WRAP, gap 20)
│       ├── Primary 色票卡 (160×200)
│       ├── Accent 色票卡 (160×200)
│       └── ... (共 11 張)
├── Typography (VERTICAL, gap 0)
│   └── 9 個 Type Row
├── Spacing (VERTICAL, gap 12)
└── Components (VERTICAL, gap 32)
    ├── Button Group
    ├── Card Demo
    └── Input Demo
```
