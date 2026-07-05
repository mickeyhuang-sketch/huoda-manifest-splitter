# 托運單拆分工具 — Railway 部署說明

這是一個純前端的靜態網頁工具（PDF拆分＋OCR辨識＋訂單比對），
所有運算都在瀏覽器端完成，不需要資料庫、不需要後端邏輯，
這個專案只是用一個極簡單的靜態伺服器把 index.html 發布出去而已。

## 部署到 Railway 的步驟

### 方法一：用 Railway 網頁介面（不需要會下指令，最簡單）

1. 到 https://railway.app 註冊／登入帳號
2. 把這個資料夾（連同 `index.html`、`package.json`）上傳到一個 GitHub Repository
   （在 GitHub 網頁上新增一個 repo，把這幾個檔案拖進去上傳即可，不需要用指令）
3. 回到 Railway，點選「New Project」→「Deploy from GitHub repo」→ 選剛剛那個 repo
4. Railway 會自動偵測到 `package.json`，自動執行 `npm install` 再執行 `npm start`
5. 部署完成後，Railway 會給一個網址（例如 `xxx.up.railway.app`），開啟就能看到工具

### 方法二：用 Railway CLI（如果你朋友熟悉終端機）

```bash
npm install -g @railway/cli
railway login
cd 這個資料夾
railway init
railway up
```

部署完成後一樣會拿到一個公開網址。

## 之後要更新工具內容怎麼辦？

只要把新版的 `index.html` 覆蓋掉這個資料夾裡的檔案，重新 push 到 GitHub
（Railway 有接 GitHub 的話會自動重新部署），或是重新執行一次 `railway up` 即可。

## 注意事項

- 這個工具會從網路載入幾個外部函式庫（PDF.js、PDF-lib、JSZip、SheetJS、Tesseract.js OCR），
  所以使用者端的瀏覽器需要能連上網際網路才能正常運作。
- 所有 PDF 內容、OCR 辨識、Excel比對都是在「使用者自己的瀏覽器」裡執行，
  不會上傳到 Railway 主機，Railway 在這裡純粹只是「發送這個網頁檔案」的角色，不會經手任何資料。
