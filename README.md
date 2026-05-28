# AI 智慧會議時間媒合系統

透過連結讓所有人填寫可用時段，系統即時統計並推薦最佳開會時間。

## 功能

- **即時同步**：任何人填寫後，所有人立刻看到最新結果
- **智慧推薦**：自動計算出席率最高的時段並排行顯示
- **催票看板**：一眼看出誰還沒填、一鍵複製催票名單
- **管理模式**：新增/刪除日期與時段、管理受邀成員、清空投票

## 使用方式

### 投票者
1. 開啟分享連結
2. 在左側輸入姓名（或點擊快速填入按鈕）
3. 在右側行事曆點選可參加的時段
4. 點「送出投票」

### 發起人（管理模式）
1. 點右上角「進入管理與設定模式」
2. 可修改會議標題與說明、新增刪除日期時段、管理成員名單
3. 完成後點「完成管理設定」儲存

## 本地開發

只需一個 HTML 檔，不需要 Node.js 或建置工具，直接在瀏覽器開啟即可預覽。

```bash
open index.html
```

> 本地開啟時資料儲存在 Firebase，仍需設定好 Firebase 設定才能正常運作。

## Firebase 設定

本專案使用 Firebase Realtime Database 儲存投票資料，讓所有人即時同步。

### 1. 建立 Firebase 專案

1. 前往 [console.firebase.google.com](https://console.firebase.google.com)
2. 點「新增專案」→ 輸入專案名稱 → 建立

### 2. 建立 Realtime Database

1. 左側選單「**Realtime Database**」→「建立資料庫」
2. 選擇地區（建議亞洲：asia-southeast1）
3. 選「**以測試模式啟動**」

### 3. 取得設定值

1. 右上角齒輪 → 「專案設定」→「您的應用程式」
2. 點「新增應用程式」→ 選網頁 `</>`
3. 複製 `firebaseConfig` 內容

### 4. 填入 index.html

打開 `index.html`，找到以下區塊並填入設定：

```javascript
var firebaseConfig = {
  apiKey: "填入你的 apiKey",
  authDomain: "填入你的 authDomain",
  databaseURL: "填入你的 databaseURL",   // 必填
  projectId: "填入你的 projectId",
  storageBucket: "填入你的 storageBucket",
  messagingSenderId: "填入你的 messagingSenderId",
  appId: "填入你的 appId"
};
```

### 5. 更新安全規則（建議）

Firebase Console → Realtime Database → **Rules** → 貼上以下規則：

```json
{
  "rules": {
    "meeting-v1": {
      ".read": true,
      ".write": true
    }
  }
}
```

## 部署到 GitHub Pages

```bash
git add .
git commit -m "deploy"
git push
```

然後在 GitHub repo → Settings → Pages → Source 選 `main` branch → 儲存。

幾分鐘後即可透過以下連結分享給所有人：

```
https://<你的帳號>.github.io/<repo名稱>/
```

## 技術架構

| 項目 | 說明 |
|------|------|
| 前端 | React 18（UMD，無需建置） |
| 樣式 | Tailwind CSS（CDN） |
| 資料庫 | Firebase Realtime Database |
| 部署 | GitHub Pages |
