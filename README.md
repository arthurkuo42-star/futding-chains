# futding-chains

BNI 高雄富鼎分會 · 第 16 屆產業服務鏈公開頁。

## 用途

兩個 HTML 組成：

- [`index.html`](index.html)：可編輯版本（管理員用）
- [`viewer.html`](viewer.html)：公開唯讀版本（任何人可看）

資料儲存在 JSONBin 的 `futding-chains` bin，透過 [bni-kpi](https://github.com/arthurkuo42-star/bni-kpi) 後端代打。

## 線上網址

- 編輯：https://arthurkuo42-star.github.io/futding-chains/
- 公開：https://arthurkuo42-star.github.io/futding-chains/viewer.html

## 部署

GitHub Pages 自動部署，推 `main` 即上線。

## 後端依賴

```js
const PROXY_BASE = 'https://bni-kpi-production.up.railway.app';
const CHAINS_API = `${PROXY_BASE}/api/chains-data`;
```

- `GET /api/chains-data` — 免認證，任何人可讀
- `PUT /api/chains-data` — 需 `X-Admin-Key`（用 bni-kpi 的 `ADMIN_KEY` 值）

## 認證

編輯模式按「☁️ 儲存到雲端」時會彈視窗要求管理員金鑰，儲存於 localStorage（key: `futding_chains_admin_key`）。

若輸入錯誤會自動清快取要求重輸。

## 安全事件（2026-04-22）

早期版本把 JSONBin Master Key 硬編碼在 HTML 裡，等同於公開 JSONBin 帳號的讀寫權限。已修正：

- 兩個 HTML 改走 bni-kpi proxy
- JSONBin Master Key 已 regenerate
- 三個 Railway service 同步更新新 key

⚠️ 若日後從 git history 還原舊版本，務必先確認沒有硬編碼金鑰才能 push。

## 相關

- 後端：[bni-kpi](https://github.com/arthurkuo42-star/bni-kpi)（Private）
- 整體架構：見本機 `富鼎網站/ARCHITECTURE.md`
