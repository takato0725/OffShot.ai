# CLAUDE.md — OffShot.ai

## プロジェクト概要
**OffShot.ai** は、Z-image / Wan 両対応のアイドル日常スナップ風プロンプト自動生成ツールです。
純粋な HTML / CSS / JavaScript で構成された単一ファイルアプリ（`index.html`）です。

## 技術スタック
- **HTML / CSS / JavaScript** のみ（ビルドツール・フレームワーク不要）
- 外部ライブラリなし（Google Fonts CDN のみ）
- APIキー不要・バックエンド不要
- `localStorage` でカスタムカテゴリを永続化

## ファイル構成
```
offshot-ai/
├── index.html   ← アプリ本体（全機能がこの1ファイルに集約）
├── README.md
└── CLAUDE.md
```

## コードの主要構造（index.html 内）

### データ定義
- **`PARAMS`** オブジェクト — 各パラメータのラベルと選択肢（日本語UI用）
- **`TEXT`** オブジェクト — 各パラメータの英語プロンプトテキストマップ
- 組み込みパラメータ: `location`, `distance`, `angle`, `exposure`, `hair`, `outfit`, `noise`, `motion`

### プロンプト生成関数
- `buildZPrompt(rt, customPart)` — Z-image 用プロンプトを組み立て
- `buildWanPrompt(rt, customPart)` — Wan 用プロンプトを組み立て
- `generate()` — UIの状態を読み取りプロンプトを生成・表示

### カスタムカテゴリ
- `customCategories` 配列（`localStorage` に `'idol_snap_custom'` キーで保存）
- 追加・編集・削除は `saveCategory()` / `deleteCategory()` で管理

## 修正時の注意事項

### やってよいこと
- `PARAMS` と `TEXT` にエントリを追加してパラメータを増やす
- `buildZPrompt` / `buildWanPrompt` のテンプレートを調整する
- CSS変数（`:root`）を変更してテーマカラーを調整する

### やってはいけないこと
- **Pony・SDXL に関する設定・キーワードは追加しない**（対応外モデル）
- `PARAMS` のキー名を変更すると `TEXT` や `locks` との整合性が崩れる
- `localStorage` のキー `'idol_snap_custom'` を変更するとユーザーデータが失われる

## 対応モデル

| モデル | 用途 |
|---|---|
| **Z-image** | 静止画生成 |
| **Wan** | 動画生成 |
