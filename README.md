# Figma 設計規格產生器（figma-design-generator）

整合 **frontend-design** 美學準則、**theme-factory** 主題思維，以及 **TalkToFigma MCP** 的 **Agent Skill**：從設計規格文件 → 靜態預覽網頁 → 在 Figma 中自動繪製 UI。

## 三階段流程

```
Phase 1：設計規格與視覺分析  →  design-spec.md
Phase 2：靜態高標預覽網頁    →  preview.html（純 HTML + CSS）
Phase 3：Figma 精準繪製      →  TalkToFigma MCP
```

| 階段 | 重點 |
|------|------|
| **Phase 1** | 釐清主題、元件範圍、色彩偏好；定義色彩／字型／間距／圓角等 Token，並依模板產出 `design-spec.md`。 |
| **Phase 2** | 依規格產出含色票、字型、間距與元件展示的靜態頁；使用 CSS Variables、Google Fonts、響應式排版。 |
| **Phase 3** | 在 Figma 已開啟文件且 TalkToFigma 連線的前提下，依 MCP 流程建立 Frame、填入文字與色彩（Hex 需換算為 Figma 0–1 RGB）。 |

完整準則、繪製順序與品質要求見 [`SKILL.md`](SKILL.md)。

## 核心理念：高擬真還原

針對參考圖或複雜 UI，強調複合元件拆解、狀態與層次、徽章與指標獨立 Frame、圖示與數據裝飾完整性等，避免「只畫示意」。細項條列於 `SKILL.md` 的「通用高擬真還原」章節。

## 適用情境（觸發關鍵詞）

例如：設計規格、Figma 繪製、UI 元素配置、色彩／設計系統、元件規格、figma-mcp、產出 Figma、UI 元件庫等。完整列表見 [`SKILL.md`](SKILL.md) 的 frontmatter `description`。

## 前置條件（Phase 3）

- 使用者於 **Figma** 中開啟目標文件。  
- **TalkToFigma** 外掛已連線，且 MCP 可用。  

工具呼叫順序與參數說明見 [`references/figma-mcp-guide.md`](references/figma-mcp-guide.md)。

## 參考文件

| 檔案 | 用途 |
|------|------|
| [`references/design-spec-template.md`](references/design-spec-template.md) | `design-spec.md` 章節結構與 Token 表格 |
| [`references/figma-mcp-guide.md`](references/figma-mcp-guide.md) | TalkToFigma MCP 工具與範例 |
| [`references/figma-element-mapping.md`](references/figma-element-mapping.md) | HTML／設計元素與 Figma 節點對應 |
| [`assets/design-spec-example.md`](assets/design-spec-example.md) | 規格填寫範例 |

## 目錄結構

```
figma-design-generator/
├── README.md
├── SKILL.md
├── references/
│   ├── design-spec-template.md
│   ├── figma-mcp-guide.md
│   └── figma-element-mapping.md
└── assets/
    └── design-spec-example.md
```

## 授權與貢獻

若本技能隸屬於上層儲存庫，請依該儲存庫的授權與貢獻指南為準。
