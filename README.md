# Cassell Teng｜鄧棋耀個人作品集

以單頁網站呈現鄧棋耀（Cassell Teng）的專業背景、代表專案與參與作品，涵蓋日本動畫背景美術、遊戲企劃、跨國專案管理、日文商務溝通及 IP 授權，並介紹目前持續精進的 AI 專案管理方向。

[LinkedIn](https://www.linkedin.com/in/cassellteng) · [Behance 作品集](https://www.behance.net/cassellteng)

## 關於這個專案

本專案是以繁體中文製作的個人履歷與作品集網站，讓招募團隊、合作夥伴與對動漫遊戲產業感興趣的訪客，快速了解我的經歷與專業能力。

網站採用 HTML、Tailwind CSS 與原生 JavaScript 製作，主要版面、作品資料與互動邏輯集中在 `index.html`，不需要安裝 npm 套件或執行建置流程。

## 網站內容

- **關於我**：十年以上台日動漫與遊戲產業經歷，以及跨領域職涯介紹。
- **重點代表作**：《百劍討妖傳綺譚》、《出包王女 DARKNESS 真實公主》及日本動畫背景美術經歷。
- **參與作品庫**：整合遊戲製作、遊戲營運／社群與背景美術作品。
- **核心職能**：日文商務溝通、AI 專案管理、遊戲企劃、營運分析、IP 授權與動畫美術。
- **常見問題與合作形式**：介紹可洽談的職務、專案及合作方向。

## 主要功能

| 功能 | 說明 |
| --- | --- |
| 響應式版面 | 配合桌面、平板與手機尺寸調整內容，提供行動版導覽選單 |
| 深淺色切換 | 首次載入參考系統偏好，並透過 `localStorage` 保存選擇 |
| 作品搜尋與分類 | 依作品名稱或描述搜尋，並搭配作品類別篩選 |
| 背景音樂 | 點擊播放或暫停，搭配播放狀態與波形動畫 |
| 聯絡表單 | 以彈出視窗收集姓名、電子信箱、主旨與留言，送至 Google Apps Script 端點 |
| 網頁 HTML 下載 | 將當下頁面的 HTML 匯出為 `index.html` |
| 搜尋與分享資訊 | 包含 SEO meta 標籤、Open Graph，以及 Person／FAQPage JSON-LD 結構化資料 |

## 技術組成

| 技術 | 用途 |
| --- | --- |
| HTML5 | 頁面結構、表單與音訊元件 |
| Tailwind CSS（CDN） | 響應式版面、配色與深色模式 |
| 原生 JavaScript | 作品渲染、搜尋篩選、主題切換與表單提交 |
| Font Awesome 6.4.0（CDN） | 介面圖示 |
| Google Apps Script | 外部聯絡表單接收端 |

前端頁面不需要自行架設應用程式伺服器；聯絡表單則依賴另外部署的 Google Apps Script 服務。

## 檔案配置

將本 README 與網站檔案放在同一層：

```text
.
├── index.html    # 網站版面、樣式設定、作品資料與互動邏輯
└── README.md     # 專案說明
```

圖片、音樂、Tailwind CSS 與圖示樣式目前由外部網址載入。Google Apps Script 後端程式不包含在 `index.html` 中。

## 本機預覽

1. 下載儲存庫內容。
2. 使用現代瀏覽器開啟 `index.html`。
3. 保持網路連線，以載入外部樣式、圖示、圖片與音樂。

也可以使用編輯器提供的本機靜態網站預覽功能開啟頁面。預覽版面與作品搜尋不需要提交聯絡表單。

## 內容維護

主要修改位置皆位於 `index.html`：

| 修改項目 | 對應位置 |
| --- | --- |
| 網站標題與搜尋摘要 | `<title>`、description 與其他 meta 標籤 |
| 社群分享資訊 | Open Graph 標籤；`og:url` 可改為實際網站網址 |
| 個人結構化資料 | `application/ld+json` 中的 Person 與 FAQPage |
| 自我介紹與代表作 | `#about`、`#milestones` 區塊 |
| 作品清單 | JavaScript 的 `worksData` 陣列 |
| 專業技能與問答 | `#skills`、`#faq` 區塊 |
| 個人照片與作品圖片 | 對應 `<img>` 的 `src` 與 `alt` |
| 背景音樂 | `#bgm-player` 內的 `<source>` |
| 聯絡表單接收網址 | `GAS_ENDPOINT` 常數 |

新增作品時，可沿用以下資料格式：

```javascript
{
  title: "作品名稱",
  category: "dev",
  tag: "Console/PC",
  desc: "參與角色與工作內容。"
}
```

`category` 對應分類：`dev` 為遊戲製作、`ops` 為遊戲營運／社群、`art` 為背景美術。

## 聯絡表單設定與限制

表單以 `POST` 將下列欄位送至 `GAS_ENDPOINT`，內容格式為 `application/x-www-form-urlencoded`：

| 欄位 | 內容 | 必填 |
| --- | --- | --- |
| `name` | 姓名或稱呼 | 是 |
| `email` | 電子信箱 | 是 |
| `subject` | 洽談主旨 | 否 |
| `message` | 留言內容 | 是 |

若將網站改作自己的作品集，請將 `GAS_ENDPOINT` 替換為自己的接收端，並讓後端處理上述欄位。

目前提交使用 `fetch` 的 `no-cors` 模式，前端無法讀取伺服器回應來確認資料是否成功儲存。因此，畫面顯示送出成功不等同於後端已完成收件；實際結果需由接收端確認。

## 使用說明

- 網站依賴外部資源，離線時可能無法完整顯示樣式、圖示或媒體。
- 背景音樂需由使用者點擊播放，能否播放也取決於瀏覽器及音訊來源狀態。
- 「下載本頁原始碼」匯出的是當下頁面的 HTML，不會一併封裝外部圖片、音樂或服務。
- 本網站為個人作品與經歷展示；提及的遊戲、動畫及品牌不代表本儲存庫包含其原始碼或完整素材。

## 作者與聯絡

**鄧棋耀 Cassell Teng**  
跨領域動漫遊戲專案經理・AI 專案管理

- [LinkedIn](https://www.linkedin.com/in/cassellteng)
- [Behance](https://www.behance.net/cassellteng)
- 網站內的「線上表單聯絡我」

## 版權與授權

網站頁尾標示 © 2026 鄧棋耀 Cassell Teng. All rights reserved.

本 README 不另行授予程式碼或素材的使用授權。第三方套件依各自授權條款使用；網站中涉及的遊戲、動畫名稱、商標、圖片與音樂，其權利歸各權利人所有。
