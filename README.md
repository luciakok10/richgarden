# 晴山御花園 RICH GARDEN — 網站部署說明

崗石電梯豪墅 / 霧峰正市心 / 全新落成

---

## 📦 檔案結構

```
rich-garden-website/
├── index.html        ← 主頁面（已含所有 CSS/JS，單檔即可運作）
├── favicon.svg       ← 瀏覽器分頁小圖示
├── robots.txt        ← 搜尋引擎規則
├── images/           ← 所有 EDM、輪播、地標照片素材
└── README.md         ← 本說明文件
```

---

## ✅ 上架步驟（最快 3 分鐘）

1. 解壓縮這個資料夾
2. 把 `index.html`、`favicon.svg`、`robots.txt` 和 `images/` 整批上傳到您的網站根目錄
3. 用瀏覽器打開 `https://您的網域/index.html`（或設為 default index 後直接打開首頁）

支援的部署方式：
- **一般主機 / 虛擬主機**：FTP 上傳到 `public_html` 或 `www` 根目錄
- **Cloudflare Pages / Netlify / Vercel**：把整個資料夾拖進去就好
- **GitHub Pages**：推到 repo 的 `main` 分支根目錄
- **AWS S3 / GCS Static Hosting**：整批上傳並設 `index.html` 為 index document

純靜態網站，**不需要 PHP / Node / 資料庫**。

---

## ⚠️ 上架前必改的 4 個設定

以下幾處目前是「示範值」，**正式上架前請務必替換**，否則對應功能不會運作：

### 1️⃣ Google Tag Manager（追蹤碼）

**位置**：`index.html` 第 36 行 與 第 706 行附近，搜尋 `GTM-XXXXXXX` 即可定位

```html
<!-- 第 15 行 -->
})(window,document,'script','dataLayer','GTM-XXXXXXX');

<!-- 第 692 行 -->
<iframe src="https://www.googletagmanager.com/ns.html?id=GTM-XXXXXXX"
```

**做法**：把兩處 `GTM-XXXXXXX` 換成您實際的 GTM 容器 ID（格式類似 `GTM-A1B2C3D`）。

如果暫時不需要 GTM 追蹤，可以**整段 `<!-- Google Tag Manager -->` 區塊刪掉**，網站不受影響。

---

### 2️⃣ 表單收件信箱（Formspree）

**位置**：`index.html` 搜尋 `YOUR_FORM_ID`

```html
<form id="contactForm"
      action="https://formspree.io/f/YOUR_FORM_ID"
      method="POST" novalidate>
```

**做法**：
1. 到 https://formspree.io 免費註冊一個帳號（用您要收件的 email）
2. 建立一個 form，會拿到一組 ID（類似 `xnqryljk`）
3. 把 `YOUR_FORM_ID` 換成那組 ID，例如：
   ```html
   action="https://formspree.io/f/xnqryljk"
   ```
4. 之後客戶在網站填表單，內容會自動寄到您 Formspree 註冊的 email

> 不想用 Formspree 的話，也可以把 `action` 換成自己的後端 API、Google Apps Script、SendGrid 等任何能接 POST 的端點。

---

### 3️⃣ 粉絲專頁連結

**位置**：`index.html` 搜尋 `https://www.facebook.com/`

```html
<a class="action-btn" href="https://www.facebook.com/" target="_blank" ...>
```

**做法**：把 `https://www.facebook.com/` 換成您粉專的完整網址，例如：
```html
href="https://www.facebook.com/sunnymountain.tw"
```

---

### 4️⃣ OG 分享圖的網址（影響 FB / LINE 分享預覽）

**位置**：`index.html` 第 21 行附近

```html
<meta property="og:image" content="images/main-cover.jpg" />
<meta name="twitter:image" content="images/main-cover.jpg" />
```

**做法**：把相對路徑改成**完整絕對網址**，FB / LINE 才抓得到預覽圖：
```html
<meta property="og:image" content="https://您的網域/images/main-cover.jpg" />
<meta name="twitter:image" content="https://您的網域/images/main-cover.jpg" />
```

同時也建議把 `<meta property="og:url" content="https://您的網域/" />` 補上去（在 OG 區塊裡）。

---

## 🎨 客製化小指南

### 改背景紅色

`index.html` 內 `<style>` 區塊，找：
```css
body {
  background-color: #A6131C;
  ...
}
```
直接改 `#A6131C` 為您要的紅。例如：
- 較深的酒紅：`#8B0F18`
- 較鮮的中國紅：`#B81413`
- 較沉穩的暗紅：`#7E0403`

### 改頂部聯絡資訊（地址、電話）

搜尋 `霧峰區民生路 60 號` 與 `04-2330-6888` 即可找到頂部、底部、CTA 三處，一次改完。

---

## 🚀 上架後建議再做

- [ ] 替換 GTM ID（或移除 GTM 區塊）
- [ ] 設定 Formspree 並更新 `YOUR_FORM_ID`
- [ ] 替換粉專連結
- [ ] OG / Twitter 圖片改為絕對網址
- [ ] 在 Google Search Console 提交網站 + sitemap
- [ ] 用 https://developers.facebook.com/tools/debug/ 測試 FB 分享預覽
- [ ] 用 PageSpeed Insights 跑一下效能（圖片較大可考慮再壓縮）

---

## 📝 圖片優化提醒（選擇性）

`images/` 內的 JPG 大多在 3–8 MB，全頁總大小約 **54 MB**。如果用戶網路速度較慢可能載入較久。建議用工具壓縮：

- **線上**：https://tinyjpg.com（免費、品質損失極小）
- **批次**：ImageOptim（macOS）/ FileOptimizer（Windows）
- **目標**：每張 JPG < 500 KB，整頁 < 8 MB

壓縮後直接覆蓋原檔即可，不需改任何 HTML。

---

## ❓ 常見問題

**Q：在某些舊瀏覽器看，背景紅色和素材有色差。**
A：JPG 的紅是 sRGB 色域，CSS 的 `#A6131C` 也是 sRGB，理論上應一致。若有色差，多半是螢幕色彩管理問題，可改 `body { background-color: ... }` 微調到肉眼無感的差異。

**Q：手機上看到下方的「立即預約賞屋」浮動按鈕擋到內容。**
A：可在 CSS 中找 `.mobile-cta` 並調整 `bottom` 數值，或把 `body { padding-bottom: 70px; }` 加大。

**Q：表單送出後顯示「送出失敗」。**
A：99% 是 Formspree 還沒設定（`YOUR_FORM_ID` 沒換）。請參考上面第 2️⃣ 項。

---

## 📄 授權

本網站之素材（圖片、文案、品牌標誌）著作權歸晴山建設股份有限公司所有。

---

如有任何技術問題，可在瀏覽器按 F12 打開開發者工具的 Console 看錯誤訊息，多半能直接看出原因。
