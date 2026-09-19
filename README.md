# 夜燈氛圍光

投影機用的氛圍夜燈網頁：星空、壁爐、星空營火三種模式，亮度與速度可調，可設定 30/60/90 分鐘後自動變暗。沒有任何聲音，所以可以一邊用 Spotify 放音樂。

## 部署到 GitHub Pages

1. 在 GitHub 建一個新的 repository，名稱隨意，設為 Public。
2. 把這個資料夾裡的所有檔案上傳到 repository 根目錄（Add file → Upload files，整批拖進去）。
3. 進 Settings → Pages，Source 選 **Deploy from a branch**，branch 選 **main**、資料夾選 **/ (root)**，按 Save。
4. 等一兩分鐘，網址會是 `https://<你的帳號>.github.io/<repo 名稱>/`。

## 加到手機主畫面（全螢幕的關鍵）

- **iPhone**：用 Safari 開上面的網址 → 分享 → 加入主畫面。從主畫面圖示打開就沒有網址列。
- **Android**：用 Chrome 開 → 選單 → 安裝應用程式／加到主畫面。

## 檔案說明

| 檔案 | 用途 |
| --- | --- |
| `index.html` | 網頁本體，所有程式和樣式都在裡面 |
| `manifest.webmanifest` | 讓它能以 App 形式安裝、預設橫向全螢幕 |
| `sw.js` | 離線快取，裝好之後沒網路也能開 |
| `icon-192.png` / `icon-512.png` | 主畫面圖示 |
| `.nojekyll` | 讓 GitHub Pages 原樣輸出檔案 |

## 改版後要注意

改了 `index.html` 之後，把 `sw.js` 第一行的 `ambient-v1` 改成 `ambient-v2`（每次改都換個號碼），否則已經安裝的裝置會繼續用舊的快取版本。
