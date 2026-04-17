# 外浦海岸マップ（Sotoura Map）

Google スプレッドシートをマスタとし、**イラストマップ画像**（`map/map.png`）上に店舗ピンを表示するシングルページアプリです。  
Mapbox GL JS の **空白スタイル**に画像を重ね、**世界地図を主表示にしません**。

---

## ドキュメント

| ドキュメント | 内容 |
|--------------|------|
| [docs/REQUIREMENTS.md](docs/REQUIREMENTS.md) | 要件定義 |
| [docs/SPREADSHEET.md](docs/SPREADSHEET.md) | **スプレッドシート列仕様（マスタ）** |
| [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md) | モジュール構成とデータフロー |
| [docs/EMBEDDING.md](docs/EMBEDDING.md) | 観光協会サイトへの iframe 埋め込み |
| [docs/OPERATIONS.md](docs/OPERATIONS.md) | 運用・デプロイ・外部サービス |
| [docs/samples/spreadsheet-headers.csv](docs/samples/spreadsheet-headers.csv) | 新規シート用ヘッダー行 |

---

## 主な機能

- **イラストマップ**: `mapbox://styles/mapbox/empty-v9` + `map.png`（地理参照は `CONFIG.MAP_IMAGE`）
- **店舗データ**: Google Sheets を JSONP（gviz）で取得。住所・電話（日英）、`store_id`、カテゴリ、詳細、クーポン、ニュース等
- **UI**: カテゴリ絞り込み、レイヤー表示切替（ピン / ルート / エリア枠）、カード一覧（PC では折りたたみ可能なサイドバー）、詳細モーダル、ニュースティッカー、日英切替、現在地（任意）
- **更新**: 既定 30 秒ポーリング、差分があれば再描画。`?refresh=1` で強制再取得
- **計測**: Google Analytics（プレースホルダ ID を本番用に差し替え）

---

## セットアップ

1. [map/index.html](map/index.html) を開き、以下を設定する。
   - `CONFIG.MAPBOX_TOKEN` — Mapbox アクセストークン
   - `CONFIG.SHEET_ID` — スプレッドシート ID
   - 必要に応じて `CONFIG.POLL_INTERVAL`（`0` でポーリング停止）
2. スプレッドシートは [docs/SPREADSHEET.md](docs/SPREADSHEET.md) の列定義に合わせ、**リンクを知っている全員が閲覧可**など gviz が読める公開設定にする。
3. `map.png` / `map.pgw` と同じディレクトリに `index.html` を置くか、パスを合わせる。

静的ファイルとして任意の HTTPS ホストに配置可能です。

---

## 技術スタック

- Mapbox GL JS 3.x
- Google Sheets（Visualization API / JSONP）
- ビルド不要（単一 HTML）

---

## 注意

- Mapbox・Google の利用規約・料金に従ってください。
- 公開スプレッドシートに載せる個人情報の範囲は運用で管理してください。
- Geolocation は HTTPS 推奨。
