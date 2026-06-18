# 筋トレ記録アプリ 💪

完全個人用の筋トレ記録 PWA。GitHub Pages でホスティングし、記録は GitHub API
経由でこのリポジトリの `data/records.json` に直接保存します。

公開URL: **https://culapy1995.github.io/training/**

## 機能

- 📅 **カレンダー** … 月表示・記録のある日にドット・スワイプで月移動
- ✏️ **記録** … 部位別に種目を複数選択 → 3セット（kg・回数をタップ入力）→ 保存
  - kg は 2.5kg刻み（2.5〜100kg）、回数は 1〜15 をタップ選択
  - 前回値を自動コピー
  - 懸垂・ディップスは「サポート(kg)」扱い（自重=0 も記録可）
  - 🏃 ランニング（傾斜・時間）も記録可
- 📊 **レポート** … 部位別頻度（直近30日）＋種目別の重量推移（直近3ヶ月／Chart.js）
- ⚙️ **設定** … トークン／リポジトリ設定・JSON エクスポート／インポート・データリセット

## 構成

```
/
├── index.html        メインアプリ（HTML + CSS + JS 単一ファイル）
├── manifest.json     PWA 設定
├── service-worker.js オフラインキャッシュ（閲覧のみ）
├── icon-192.png      PWA アイコン
├── icon-512.png      PWA アイコン
└── data/
    └── records.json  記録データ（GitHub API 経由で書き込み）
```

## セットアップ

### 1. GitHub Pages を有効化

リポジトリの **Settings → Pages** で、Source を `Deploy from a branch`、
Branch を `main`（公開したいブランチ）/ `root` に設定して保存します。
数分後に `https://culapy1995.github.io/training/` で公開されます。

### 2. アクセストークンを作成

記録の書き込みには、このリポジトリの **Contents（読み書き）** 権限を持つトークンが必要です。

- **Fine-grained token（推奨）**: GitHub → Settings → Developer settings →
  Fine-grained tokens → このリポジトリを対象に、**Repository permissions › Contents: Read and write** を付与
- もしくは **Classic token**: `repo` スコープを付与

### 3. アプリで初期設定（初回のみ）

1. 公開URLを開く
2. **設定（⚙️）** タブを開く
3. 「GitHubアクセストークン」に作成したトークンを貼り付け
4. 「リポジトリ名」が `culapy1995/training` であることを確認
5. **保存して接続** をタップ

トークンは端末内（`localStorage`）にのみ保存され、以降の入力は不要です。
`data/records.json` が無い場合は初回保存時に自動作成されます。

### 4. ホーム画面に追加（PWA）

iPhone Safari で公開URLを開き、共有 → **ホーム画面に追加**。
フルスクリーンのアプリとして起動できます（オフラインでは閲覧のみ）。

## バックアップ

設定タブから記録を JSON でエクスポート／インポートできます。
データは常に GitHub 上の `data/records.json` にも保存されます。

## 技術

HTML / CSS / JavaScript（フレームワークなし）・Chart.js（CDN）・GitHub API v3・
localStorage・PWA（manifest + service worker）。
