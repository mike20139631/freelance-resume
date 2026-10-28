# Git 初始化與 GitHub Pages 發布

`information_engineering_freelance_resume.html` 是靜態網頁：不需要後端或建置流程，可部署到 GitHub Pages。深色模式使用瀏覽器的 `localStorage`，不需要伺服器。不過頁面透過 CDN 載入 Tailwind CSS 與 Google Fonts，訪客需要能連上這些服務才能看到完整樣式與字型。

## 初始化並上傳

在此專案目錄開啟終端機，依序執行：

```bash
git init -b master
git add .
git commit -m "初次提交：新增接案履歷與 GitHub Pages 設定"
```

接著在 GitHub 建立一個**空白儲存庫**（不要勾選自動建立 README、`.gitignore` 或 License），將下列 `<你的帳號>` 和 `<儲存庫名稱>` 換成實際值：

```bash
git remote add origin https://github.com/<你的帳號>/<儲存庫名稱>.git
git push -u origin master
```

首次提交前，請先確認履歷上所有公開資料都適合讓任何人檢視；GitHub Pages 與 Git 歷史都不適合存放密碼或金鑰。

## 啟用 GitHub Pages

1. 進入儲存庫的 **Settings → Pages**。
2. 在 **Build and deployment** 選擇 **Deploy from a branch**，選擇 `master` 分支及 `/ (root)` 資料夾，按 **Save**。
3. 部署完成後，開啟：

   `https://<你的帳號>.github.io/<儲存庫名稱>/`

根目錄的 `index.html` 會在瀏覽器中自動轉導到 `information_engineering_freelance_resume.html`。之後若要改用其他版面，將新 HTML 檔案放在根目錄，並同時修改 `index.html` 的 `<meta http-equiv="refresh">` 目標及頁面中的備援連結即可，不必複製整份履歷。這是瀏覽器端轉導，網址列會顯示實際履歷檔案的網址，並非伺服器的 HTTP 301/302 轉址。

之後更新網頁時：

```bash
git add .
git commit -m "更新接案履歷"
git push
```
