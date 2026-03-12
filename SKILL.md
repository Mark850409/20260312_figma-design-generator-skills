---
name: figma-design-generator
description: 整合設計美學與 Figma MCP 的完整設計工作流程技能。當使用者需要：(1) 建立 Figma 設計規格文件、(2) 產生含色彩/字型/元件的設計系統、(3) 將設計規格轉換為靜態預覽網頁、(4) 使用 TalkToFigma MCP 在 Figma 中自動繪製 UI 元素、(5) 建立 UI 元件庫或設計系統時觸發。關鍵詞包含：「設計規格」、「Figma 繪製」、「UI 元素配置」、「色彩系統」、「設計系統」、「元件規格」、「figma-mcp」、「產出 Figma」。
---

# Figma 設計規格產生器

整合 frontend-design 美學準則、theme-factory 主題系統、TalkToFigma MCP 的完整三階段設計工作流程。

## 工作流程概覽

```
Phase 1: 設計規格與視覺分析 → design-spec.md
Phase 2: 靜態高標預覽網頁 → preview.html
Phase 3: Figma 精準繪製 → TalkToFigma MCP
```

## 核心準則：100% 視覺還原
### 核心準則：通用高擬真還原 (Universal High-Fidelity)
無論輸入何種 UI 模板圖檔，必須遵循以下「像素級」原則：
- **複合組件深度拆解**：不要用標籤替代複雜的 UI 構造。例如：
    - **搜尋/輸入框**：應還原其具體的 Border-radius、內邊距、以及附屬的按鈕/圖標組件。
    - **選單系統**：精確複製側邊欄或頂欄的垂直/水平層次，包含子選單的縮排、前綴圖標與展開指示符。
- **動態狀態與視覺層次**：
    - 活動 (Active) 或 懸停 (Hover) 狀態應具備獨立的背景 Frame、半透明色彩疊加及圓角。
    - 關鍵文字與圖標在不同狀態下的顏色對比度應嚴格對照原圖。
- **精確徽章與通知指標 (Indicators)**：
    - 各類 Badge (如 "New", 數量標記) 必須作為獨立的圓角矩形 Frame 建構，而非僅是文字。
    - 文字應在徽章內部水平垂直居中，字號應微調至與原圖比例一致。
- **視覺一致性指標**：
    - **圖標一致性**：使用 Unicode 符號時，必須挑選視覺權重與形態最接近原圖的符號組。
    - **數據裝飾**：圖表中的網格線、座標軸數值、以及卡片背景的淡化裝飾圖標必須全數繪製。
3. **圖標處理**：若無 SVG，使用 Lucide-like Unicode 圖標或簡單幾何圖形組合重現實例。
4. **完整性**：必須繪製整個畫板，不得只繪製「示範」元件。

---

## Phase 1：設計規格制定

### 1-1 需求釐清

向使用者確認：
- **設計主題**：專案名稱與風格方向（科技/自然/金融/時尚⋯）
- **元件範圍**：需要哪些元件（按鈕/卡片/輸入框/導覽列⋯）
- **色彩偏好**：已有品牌色或交由 AI 選擇？

### 1-2 色彩系統設計

定義六種顏色角色（參見 `references/design-spec-template.md`）：
- `primary`、`primary-hover`、`secondary`、`accent`
- `background`、`surface`、`text-primary`、`text-secondary`、`border`
- `success`、`warning`、`error`

色彩選擇原則（取自 frontend-design 技能）：
- **禁止**：過度使用 Purple Gradient (#7C3AED 系列) 和白底通用色
- **建議**：選擇具有強烈個性的主色，搭配一個對比強烈的 Accent 色
- 確保 WCAG AA 對比比例（文字 4.5:1 以上）

### 1-3 字型系統設計

定義三層字型角色（Google Fonts 優先）：
- **Display**：品牌標題字（24–64px），選擇具有獨特個性的字體
- **Body**：正文字體（14–18px），可讀性優先
- **Mono**：程式碼字體（必要時）

**禁止**使用 Inter、Roboto、Arial 等通用字體。

### 1-4 間距與圓角

```
Spacing: 4 / 8 / 12 / 16 / 24 / 32 / 48 / 64px
Border Radius: none(0) / sm(4) / md(8) / lg(16) / full(9999)
Shadows: sm / md / lg / xl
```

### 1-5 產出設計規格文件

使用 `references/design-spec-template.md` 的格式，產出完整的 `design-spec.md` 文件。

---

## Phase 2：靜態預覽網頁

依據 Phase 1 的設計規格，生成一個完整的靜態 HTML 預覽頁面：

### 必要區塊

1. **Color Palette 展示**：每個顏色角色的色票 + Hex Code + 名稱
2. **Typography 展示**：各字體角色的樣本文字（Display/Heading/Body/Caption）
3. **Spacing Scale 展示**：間距視覺化條狀圖
4. **元件展示**：使用者指定的所有元件的視覺呈現

### 技術規範

- 純 HTML + CSS（不依賴外部框架）
- 使用 CSS Variables 儲存所有設計 Token
- 透過 `<link>` 載入 Google Fonts
- 響應式排版

### 美學標準（取自 frontend-design 技能）

- 選擇清晰的美學方向並一致執行
- 運用非對稱排版、負空間、視覺層次
- 加入細微的 hover 動效與過場動畫

---

## Phase 3：Figma 自動繪製

> **前提**：使用者必須在 Figma 中開啟任一文件，且 TalkToFigma 插件已連線。

詳細 MCP 工具使用方式請參閱 `references/figma-mcp-guide.md`。

### 繪製順序

```
1. get_document_info()         → 確認已連線
2. join_channel()              → 加入頻道
3. 建立主 Frame（設計規格展示頁）
4. 依序建立各子區塊 Frame
5. 填入文字、色彩、元件
```

### Figma 色彩格式換算

Figma 使用 0–1 範圍的 RGB，NOT 0–255：
```
r = hex_r / 255
g = hex_g / 255
b = hex_b / 255
```

### 標準繪製結構

詳見 `references/figma-element-mapping.md` 的元素對應表。

---

## 技能參考文件

- **MCP 完整用法**：參閱 `references/figma-mcp-guide.md`（包含所有 TalkToFigma 工具說明與範例）
- **規格文件模板**：參閱 `references/design-spec-template.md`
- **HTML→Figma 對應**：參閱 `references/figma-element-mapping.md`
- **規格範例**：參閱 `assets/design-spec-example.md`
