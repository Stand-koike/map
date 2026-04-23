# map/ — アプリ本体フォルダ

このフォルダには外浦海岸マップの **全リソース** が入っています。  
ブラウザで `index.html` を開くか、ローカルサーバー経由でアクセスしてください。

---

## ファイル一覧

| ファイル | 説明 |
|----------|------|
| `index.html` | アプリ本体（単一 HTML・ビルド不要） |
| `map.png` | イラストマップ画像（937×755 px） |
| `map.wld` | `map.png` の地理参照ファイル（EPSG:3857） |
| `map.png.aux.xml` | GDAL メタデータ（参考情報） |

---

## 起動方法

### ローカルサーバー（推奨）

`file://` 直接開きだと WebGL テクスチャの読み込みが Chrome でブロックされる場合があります。  
Python が入っている場合は以下で簡易サーバーを立ち上げてください：

```bash
cd map
python -m http.server 8080
```

ブラウザで `http://localhost:8080` を開く。

### VS Code Live Server

VS Code の **Live Server** 拡張機能を使う場合は `index.html` を右クリック →「Open with Live Server」。

---

## 初期設定

`index.html` 冒頭の `CONFIG` オブジェクトを編集します：

```js
const CONFIG = {
    MAPBOX_TOKEN: 'pk.YOUR_TOKEN_HERE',   // Mapbox アクセストークン
    SHEET_ID:     'YOUR_SHEET_ID_HERE',   // Google スプレッドシート ID
    POLL_INTERVAL: 30000,                 // ポーリング間隔(ms)。0 で無効
    ...
};
```

スプレッドシートの列仕様は [`../docs/SPREADSHEET.md`](../docs/SPREADSHEET.md) を参照。

---

## UI 機能（PC）

| 機能 | 操作 |
|------|------|
| カードパネル折りたたみ | パネル右端の `‹ ›` ボタンをクリック |
| カテゴリ絞り込み | 左上「絞り込み」ボタン |
| レイヤー切替 | 左上「レイヤー」ボタン |
| 詳細表示 | カードまたはピンをクリック |
| 言語切替（日/英） | 左上「JP」ボタン |
| 現在地表示 | 右下の GPS ボタン |

---

## map.png の差し替え

1. 新しい画像を `map.png` として保存（同解像度推奨）
2. `map.wld`（ワールドファイル）を新しい画像に合わせて更新
3. `index.html` の `CONFIG.MAP_IMAGE.coordinates` を四隅座標に合わせて修正

詳細は [`../docs/ARCHITECTURE.md`](../docs/ARCHITECTURE.md) を参照。
