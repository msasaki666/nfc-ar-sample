# nfc-ar-sample

このリポジトリは、NFC タグにトークン付き URL を書き込み、その URL を開いた先でトークンと日付に基づく簡易なお守り（SVG）を生成・表示するデモです。ローカルでは単一の静的サーバで動作確認できます。

## 機能概要
- トップページ（`index.html`）でトークンから URL を生成
- Web NFC が使える環境では URL を NFC タグへ書き込み
- 表示ページ（`secret.html`）でトークンと当日の日付に基づき色・図形・運勢を決定し SVG を描画
- 表示中の SVG を画像（PNG）として保存

## ディレクトリ構成
- `index.html`: URL 生成と Web NFC 書き込みを行うページ
- `secret.html`: トークンでお守りを生成・表示するページ
- `package.json`: ローカル開発用スクリプト
- `pnpm-lock.yaml`: 依存ロックファイル

## 必要要件
- Node.js 18 以上推奨
- pnpm 8 以上（スクリプト内で `pnpx` を使用）
  - 未インストールの場合は: `npm i -g pnpm`

## セットアップ & 実行
1. 依存関係のインストール
   - `pnpm install`
2. 開発サーバの起動（単一サーバ）
   - `pnpm dev`
   - `http://localhost:3000` で `index.html` と `secret.html` を提供

注: スクリプトは `pnpx http-server` を使っているため、初回起動時に `http-server` を自動取得します。もし npm を使いたい場合は `package.json` のスクリプトを `npx http-server` に読み替えてください。

## 使い方
1. `http://localhost:3000` を開く
2. 任意のトークン（英数字など）を入力し「URL生成」
3. Web NFC 対応端末・ブラウザ（Chrome/Android など、HTTPS 環境が必要）では「タグに書き込む」で URL を NFC タグへ書き込み
4. 生成された URL（例: `http://localhost:3000/secret.html?t=xxxx`）を開くと、その日の運勢や図形・色でお守りが表示されます
5. 「画像保存」で PNG として保存可能

## 注意事項 / 制約
- Web NFC は対応ブラウザ・端末・HTTPS 環境でのみ動作します。ローカル開発では NFC 書き込みは表示されない場合があります（フォールバック案内を表示）。
- 本デモの「トークン」は機密情報ではありません。`secret/` 側はクライアントのみで処理しており、サーバ検証は行っていません。

## デプロイのヒント
- 静的ホスティング（GitHub Pages / Vercel / Netlify など）でリポジトリ直下の `index.html` と `secret.html` を配信できます。
- Web NFC を使うページは HTTPS 配信にしてください。

## 開発メモ
- 主要スクリプト
  - `pnpm dev`: ルートを 3000 番で起動
- 補足
  - `http-server` を `pnpx` 経由で取得・起動

## ライセンス
- `package.json` の記載に従い ISC ライセンス
