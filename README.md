# 基隆親友中秋烤肉 報名網頁

**網址：https://evan-yufanlin.github.io/keelung-bbq/**

2026/09/26（六）基隆親友中秋烤肉的報名與物資認領頁面。
純靜態網頁（GitHub Pages）+ Firebase Firestore + 匿名驗證，架構與 [樹林金蘭會館版](https://github.com/evan-yufanlin/jinlan-bbq) 相同，但使用獨立的 GitHub repo 與 Firebase 專案。

## 檔案

| 檔案 | 用途 |
|---|---|
| `index.html` | 整個網頁（含 CSS 與 JS），Firebase SDK 由 CDN 載入 |
| `firestore.rules` | Firestore 安全規則，需貼到 Firebase Console → Firestore → 規則 |

## Firestore 資料結構

| Collection | 欄位 | 說明 |
|---|---|---|
| `headcounts` | `name`, `adults`, `kids`, `note`, `ownerUid`, `ts`, `updatedAt` | 每組報名一筆；同名再送出 = 更新 |
| `claims` | `itemKey`(`分類key::品名`), `name`, `detail`, `ownerUid`, `ts` | 物資／工作認領，一項可多人認領 |
| `customItems` | `category`, `name`, `ts` | 使用者自行新增的品項 |

## 部署步驟

1. **Firebase**：專案 `keelung-bbq-2026`（asia-east1，匿名登入已啟用，規則已發布）。若要重建：建立新專案 → 啟用 Firestore（正式模式）→ Authentication 啟用「匿名」→ 新增 Web 應用程式，把 `firebaseConfig` 貼到 `index.html` → 把 `firestore.rules` 貼到 Firestore 規則並發布。
2. **GitHub**：repo `evan-yufanlin/keelung-bbq`，Pages 設定為 branch `main` / root。之後改完 `index.html` 直接 `git push` 即自動更新。
3. 打開 Pages 網址，狀態列顯示「即時同步中」即成功。
