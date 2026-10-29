# Git 初始化與 GitHub Pages 發布

首頁使用的 `freelance_resume_studio.html` 是靜態網頁：不需要後端或建置流程，可部署到 GitHub Pages。閱讀對象切換和深色模式都在瀏覽器端運作，不需要伺服器。它的樣式寫在頁面內，但字型由 Google Fonts 載入；若無法連上字型服務，瀏覽器會使用備援字型。`freelance_resume.html` 保留作為另一個版面（使用 Tailwind CSS CDN），`information_engineering_freelance_resume.html` 則保留作為原版。

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

根目錄的 `index.html` 會在瀏覽器中自動轉導到 `freelance_resume_studio.html`。之後若要改用其他版面，將新 HTML 檔案放在根目錄，並同時修改 `index.html` 的 `<meta http-equiv="refresh">` 目標及頁面中的備援連結即可，不必複製整份履歷。這是瀏覽器端轉導，網址列會顯示實際履歷檔案的網址，並非伺服器的 HTTP 301/302 轉址。

## 使用自有網域

若主網域（例如 `example.com`）已用於其他網站，可另用 `resume.example.com` 提供履歷，不需要更動主網域既有的 DNS 記錄。

1. 在網域的 DNS 管理介面新增 CNAME 記錄：名稱填 `resume`（依業者介面，也可能需填完整的 `resume.example.com`），目標填 `mike20139631.github.io`。
2. 到此儲存庫的 **Settings → Pages → Custom domain** 填入 `resume.example.com` 並儲存。若 GitHub 因此在遠端建立或修改 `CNAME` 檔案，繼續在本機編輯前先執行 `git pull`。
3. 等待 DNS 與憑證設定完成，在 Pages 設定中啟用 **Enforce HTTPS**，再以 `https://resume.example.com/` 測試。

如果有多個 Pages 儲存庫，每個儲存庫可以設定**不同子網域**，而 DNS CNAME 的目標可以相同：

| 儲存庫 | DNS CNAME | 該儲存庫的 Custom domain |
| --- | --- | --- |
| `freelance-resume` | `resume` → `mike20139631.github.io` | `resume.example.com` |
| `portfolio` | `portfolio` → `mike20139631.github.io` | `portfolio.example.com` |

注意事項：

- CNAME 只接受主機名稱，因此目標是 `mike20139631.github.io`，**不能**加入 `/freelance-resume` 等路徑；GitHub 會依各儲存庫設定的 Custom domain 辨識網站。
- 同一個子網域不能同時指定給兩個 Pages 儲存庫；若該子網域已有其他 DNS 記錄，先確認沒有衝突再設定。
- DNS CNAME 不會做網址轉導。若需要 `example.com/resume` 這種路徑，須由主網站設定轉址或反向代理；也可直接使用預設的 `https://mike20139631.github.io/freelance-resume/`。
- 使用 GitHub Free 時，通常需要公開儲存庫才能啟用 Pages；即使方案允許私人儲存庫部署 Pages，也不要假設網站內容只有自己看得到。公開前請確認沒有機密或不想公開的個資。

之後更新網頁時：

```bash
git add .
git commit -m "更新接案履歷"
git push
```
