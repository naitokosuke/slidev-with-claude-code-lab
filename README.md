# Slidev Monorepo

このリポジトリには 3 つの Slidev プロジェクトが含まれています。

## プロジェクト

- my-own-theme: カスタム Slidev テーマ（Deep Sea inspired theme）
- self-intro: 自己紹介プレゼンテーション
- teach-me-about-vue-router: Vue Router についてのプレゼンテーション

## 使い方

### 開発サーバーの起動

```bash
pnpm dev:my-own-theme
pnpm dev:self-intro
pnpm dev:teach-me-about-vue-router
```

### ビルド

```bash
pnpm build:my-own-theme
pnpm build:self-intro
pnpm build:teach-me-about-vue-router
```

### エクスポート

```bash
pnpm export:my-own-theme
pnpm export:self-intro
pnpm export:teach-me-about-vue-router
```

## セットアップ

```bash
# 依存関係のインストール
pnpm install
```

## 技術スタック

- [Slidev](https://sli.dev/) - プレゼンテーション作成フレームワーク
- [Vue.js](https://vuejs.org/) - フロントエンドフレームワーク
- [pnpm](https://pnpm.io/) - パッケージマネージャー（monorepo 対応）
