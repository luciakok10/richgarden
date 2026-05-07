# 晴山御花園 RICH GARDEN — 網站部署說明

崗石電梯豪墅 / 霧峰正市心 / 全新落成

---

## 📦 檔案結構

```
rich-garden-website/
├── index.html             ← 主頁面（單檔即運作）
├── favicon.svg            ← 瀏覽器分頁小圖示
├── robots.txt             ← 搜尋引擎規則
├── images/
│   ├── hero/              ← 首屏拆解後的素材
│   │   ├── logo.png       ← 「晴山御花園」logo（去背 PNG）
│   │   └── peony.png      ← 牡丹圖（去背 PNG）
│   ├── main-cover.jpg     ← 保留作為 OG 分享預覽圖
│   ├── sec-02.jpg ~ sec-08.jpg  ← 各 section 主圖
│   └── (carousel slides)  ← 輪播子圖
└── README.md              ← 本說明
```

---

## ✨ 動效設計

整頁採「沉穩奢華」風格：

**首屏 Hero**（多層拆解）
- 紅底自帶「呼吸」漸層脈動（14 秒一輪，極淡）
- Logo 慢速淡入 + 微上浮（0.3 → 1.7 秒）
- 「崗石電梯豪墅 / 霧峰正市心」逐字漸進入場（每字延遲 0.1 秒）
- 「— 全新落成 —」金線從中央向兩側展開
- 牡丹從稍微放大狀態緩緩淡入並回到原位（2.8 → 5.4 秒）

**全頁互動**
- 每段內容滾動進場（淡入 + 上移）
- 桌機滑鼠位置會帶柔金光暈跟隨（僅 hover 裝置）
- 底部三格 sticky bar（永遠可見）：
  - 立即預約賞屋｜FB 粉絲專頁｜路徑導航
  - 圖示有 hover 微浮、按鈕有金色掃光效果

**遵守 prefers-reduced-motion**：使用者作業系統若關閉動效，所有動畫自動停用。

---

## ✅ 上架步驟

1. 解壓縮資料夾
2. 整批上傳到網站根目錄
3. 用瀏覽器打開 `https://您的網域/index.html`

支援：一般主機 / Cloudflare Pages / Netlify / Vercel / GitHub Pages / AWS S3

純靜態，**不需要 PHP / Node / 資料庫**。

---

## ⚠️ 上架前必改的 4 個設定

### 1️⃣ Google Tag Manager（追蹤碼）

`index.html` 搜尋 `GTM-XXXXXXX`（兩處）→ 換成您的 GTM ID。
不需要追蹤就把 `<!-- Google Tag Manager -->` 整段刪掉。

### 2️⃣ 表單收件信箱（Formspree）

`index.html` 搜尋 `YOUR_FORM_ID`：
1. 到 https://formspree.io 免費註冊
2. 建立 form 拿到 ID（如 `xnqryljk`）
3. 替換 `YOUR_FORM_ID` 為實際 ID

### 3️⃣ 粉絲專頁連結

搜尋 `https://www.facebook.com/`（兩處：底部 bar 和 actions 區），替換為實際粉專網址。

### 4️⃣ OG 分享圖網址

搜尋 `og:image` 與 `twitter:image`，把相對路徑改成完整絕對網址：
```html
<meta property="og:image" content="https://您的網域/images/main-cover.jpg" />
```

---

## 🎨 客製化指南

**改背景紅色**：搜尋 `background-color: #A6131C` 改顏色即可。

**改聯絡資訊**：搜尋 `霧峰區民生路 60 號` 與 `04-2330-6888`。

**調整 Hero 動畫速度**：CSS 中 `.hero.in .hero-tagline .line1 span:nth-child(N)` 的 `transition-delay` 是逐字進場的時序；改小數值 = 更快進場。

**調整底部 bar**：
- HTML 編輯 `<nav class="bottom-cta">` 區塊調整文字、icon、連結
- primary 樣式（紅色高亮）可加在任一個按鈕的 class 上
- 想改成 4 格：把 grid `grid-template-columns: 1fr 1fr 1fr` 改成 `1fr 1fr 1fr 1fr`，再多加一個 `<a class="cta-btn">` 即可
- bar 高度由 `body { padding-bottom: 78px; }` 對應，改 bar 大小要同步改這個

**關掉滑鼠柔金光**：CSS 找 `.cursor-glow` 把 `display: none;` 加上去即可。

---

## 📊 效能數據

| 項目 | 大小 |
|---|---|
| HTML（含 CSS、JS） | ~57 KB |
| 首屏 hero 素材（logo + peony） | ~1.5 MB |
| 全部圖片 | ~10.6 MB |
| 全頁總大小 | ~11 MB |

每張單檔皆 < 1.5 MB，符合 GitHub 上傳限制（25 MB/檔）。

---

## ❓ 常見問題

**Q：首屏 hero 動畫太慢/太快？**
A：在 `.hero.in .hero-tagline .line1 span:nth-child(N)` 等 CSS rule 調整 `transition-delay`。Logo 進場時間在 `.hero-logo` 的 transition 屬性裡。

**Q：手機看 hero 牡丹位置怪怪的？**
A：`aspect-ratio: 520 / 924` 鎖住 hero 寬高比。如想讓手機版牡丹更小或位置不同，可在 `@media (max-width: 480px)` 內覆寫 `.hero-peony { width: ...; bottom: ...; right: ...; }`。

**Q：表單送出後顯示「送出失敗」？**
A：99% 是 Formspree 還沒設定（`YOUR_FORM_ID` 沒換）。

---

## 📄 授權

本網站之素材（圖片、文案、品牌標誌）著作權歸晴山建設股份有限公司所有。
