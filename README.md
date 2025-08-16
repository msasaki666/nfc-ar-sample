# nfc-ar-sample

このリポジトリは、NFC タグにトークン付き URL を書き込み、その URL を開いた先でトークンと日付に基づく簡易なお守り（SVG）を生成・表示するデモです。ローカルで 2 つの静的サイトをポート別に起動して動作確認できます。

## 機能概要
- お守り作成ページ（`/nfc-charm/`）でトークンから URL を生成
- Web NFC が使える環境では URL を NFC タグへ書き込み
- お守り表示ページ（`/secret/`）でトークンと当日の日付に基づき色・図形・運勢を決定し SVG を描画
- 表示中の SVG を画像（PNG）として保存

## ディレクトリ構成
- `nfc-charm/`: URL 生成と Web NFC 書き込みを行うページ（`index.html`）
- `secret/`: トークンでお守りを生成・表示するページ（`index.html`）
- `package.json`: ローカル開発用スクリプト
- `pnpm-lock.yaml`: 依存ロックファイル

## 必要要件
- Node.js 18 以上推奨
- pnpm 8 以上（スクリプト内で `pnpx` を使用）
  - 未インストールの場合は: `npm i -g pnpm`

## セットアップ & 実行
1. 依存関係のインストール
   - `pnpm install`
2. 開発サーバの起動（2 つの静的サーバを並行起動）
   - `pnpm dev`
   - `http://localhost:3000` … お守り作成（`nfc-charm/`）
   - `http://localhost:3001` … お守り表示（`secret/`）

注: スクリプトは `pnpx http-server` を使っているため、初回起動時に `http-server` を自動取得します。もし npm を使いたい場合は `package.json` のスクリプトを `npx http-server` に読み替えてください。

## 使い方
1. `http://localhost:3000` を開く
2. 任意のトークン（英数字など）を入力し「URL生成」
3. Web NFC 対応端末・ブラウザ（Chrome/Android など、HTTPS 環境が必要）では「タグに書き込む」で URL を NFC タグへ書き込み
4. 生成された URL（例: `http://localhost:3001/?t=xxxx`）を開くと、その日の運勢や図形・色でお守りが表示されます
5. 「画像保存」で PNG として保存可能

## 注意事項 / 制約
- Web NFC は対応ブラウザ・端末・HTTPS 環境でのみ動作します。ローカル開発では NFC 書き込みは表示されない場合があります（フォールバック案内を表示）。
- 本デモの「トークン」は機密情報ではありません。`secret/` 側はクライアントのみで処理しており、サーバ検証は行っていません。

## デプロイのヒント
- 静的ホスティング（GitHub Pages / Vercel / Netlify など）で `nfc-charm/` と `secret/` をそれぞれ配信できます。
- Web NFC を使うページは HTTPS 配信にしてください。

## 開発メモ
- 主要スクリプト
  - `pnpm dev`: `nfc-charm` を 3000 番、`secret` を 3001 番で同時起動
- 依存
  - `npm-run-all2`（開発用。並行実行に使用）
  - `http-server`（pnpx 経由で取得）

## ライセンス
- `package.json` の記載に従い ISC ライセンス
