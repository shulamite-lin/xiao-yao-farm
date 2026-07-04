# 逍遙農場 X 芒芒然

台南玉井小農直營的芒果產品說明頁。純靜態 HTML5 + CSS3，無框架、無建置流程，部署於 GitHub Pages。

🔗 **線上網址**：https://shulamite-lin.github.io/xiao-yao-farm/

## 特色

- 響應式版面：桌機／平板／手機皆適用，並針對手機橫放做過特別處理
- 商品展示：愛文芒果、黑香芒果（即將上市）、芒果乾，含價格表
- 快速導覽列：一鍵跳轉至「關於農場」「本季商品」「買芒果」「買芒果乾」
- 訂購流程說明：新鮮芒果（私訊 + 匯款）／芒果乾（超商取貨付款）
- SEO：完整 meta description、Open Graph、Twitter Card 標籤，圖片皆有 `alt` 文字
- 無障礙：符合 WCAG 2.1 AA（色彩對比、鍵盤 focus、螢幕報讀器語意標記）
- Google Analytics（GA4）流量分析

## 本地預覽

```bash
cd "Selling mangoes"
python3 -m http.server 8768
```

開啟 http://localhost:8768 。若 port 被佔用請換用其他號碼（8769、8770…）。

## 部署

直接 push 到 `main` branch，GitHub Pages 會自動建置部署，約 1–2 分鐘後線上生效：

```bash
git add index.html style.css images/<新圖檔>
git commit -m "說明修改內容"
git push origin main
```

## 專案結構

```
.
├── index.html      # 頁面內容（Hero、關於農場、商品、訂購、Footer）
├── style.css       # 所有樣式，色彩變數統一定義於 :root
├── images/         # 商品與 Hero 圖片
└── README.md
```

## 授權 / 聯絡

網站內容與圖片版權屬逍遙農場 X 芒芒然所有。訂購請透過頁面上的 Facebook 連結私訊。
