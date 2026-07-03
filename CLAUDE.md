# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 專案概述

逍遙農場（台南玉井）芒果產品說明頁。純靜態 HTML5 + CSS3，部署於 GitHub Pages。

- **線上網址**：https://shulamite-lin.github.io/xiao-yao-farm/
- **GitHub repo**：https://github.com/shulamite-lin/xiao-yao-farm

## 本地預覽

```bash
cd "Selling mangoes"
python3 -m http.server 8768
# 開啟 http://localhost:8768
```

若 port 被佔用請換用其他號碼（8769、8770…）。

## 部署

直接 push 到 main branch 即可，GitHub Pages 約 1–2 分鐘後生效：

```bash
git add index.html style.css images/<新圖檔>
git commit -m "說明修改內容"
git push origin main
```

## 取得 Facebook 圖片

FB 有反爬機制，需透過 **Playwright MCP** 在已登入的瀏覽器中用 fetch API 取得圖片：

```js
// 在 browser_evaluate 中執行
const resp = await fetch('https://scontent.xx.fbcdn.net/...');
const buf = await resp.arrayBuffer();
const b64 = btoa(String.fromCharCode(...new Uint8Array(buf)));
```

取得 base64 字串後用 Python 解碼存檔：

```python
import base64
with open('images/xxx.jpg', 'wb') as f:
    f.write(base64.b64decode(b64_string))
```

## 圖片裁切

使用 Python PIL 裁切（座標系：左上為原點）：

```python
from PIL import Image
with Image.open('images/mango2.jpg') as img:
    w, h = img.size  # 2048x1478
    crop = img.crop((x1, y1, x2, y2))
    crop.save('images/output.jpg', quality=90)
```

**現有圖片說明**：
- `hero2.jpg` — Hero banner（農夫套袋作業）
- `mango2.jpg` — 愛文（左半）+ 黑香（右半）合照原圖 2048×1478
- `mango-irwin-crop.jpg` — 愛文裁切（x=200–1024，y=0–960），`top center`
- `mango-black-crop.jpg` — 黑香裁切（x=1024–1940，y=0–1359），`center 65%`
- `dried-new.jpg` — 芒果乾近拍（現役）
- `dried2.jpg`、`dried-crop.jpg`、`extra.jpg`、`hero.jpg`、`mango-irwin.jpg` — 舊圖，已不使用
- `new-*-b64.txt` — 下載過程暫存檔，無法刪除（rm 指令被封鎖）

CSS 背景圖換新版後記得加 `?v=N` 強制清除瀏覽器快取：

```css
.black-img { background: ... url('images/mango-black-crop.jpg?v=3') ... }
```

## 架構

單頁面，四個區塊由上至下：

| 區塊 | id | 說明 |
|------|----|------|
| Hero | `#hero` | 全寬背景圖 + 品牌故事（桌機左下角，手機隱藏） |
| 商品 | `#products` | 三欄 grid：愛文、黑香（即將上市）、芒果乾 |
| 訂購 | `#order` | 兩欄 grid：新鮮芒果流程、芒果乾流程 |
| Footer | `footer` | 農場標語 + FB 連結 |

CSS 變數定義於 `:root`（`--orange`、`--green`、`--text` 等），所有色彩統一由此控制。

## 待更新內容

- **黑香芒果價格**：目前顯示「即將上市」，待確認價格後補上價格表（參考愛文的 `price-table` 結構）
- **LINE 聯絡人**：目前使用 `kib56056`，如有變更需更新兩處 `btn-group` 的 href

## 注意事項

- `rm` 指令在此專案被封鎖，無法刪除檔案
- 社群媒體圖片（FB）必須用 Playwright MCP，不可用 Firecrawl
- 修改 CSS 後若瀏覽器顯示舊版，在 `<link rel="stylesheet">` 加 `?v=N` 可強制重載
