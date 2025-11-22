# Portfolio

Hugoで構築したポートフォリオサイトです。

## 構成

- **自己紹介ページ** (`/about/`): スキルや経歴の紹介
- **ブログ** (`/blog/`): 技術記事や学びの記録
- **Products** (`/products/`): 開発したプロダクトの紹介

## 技術スタック

- [Hugo](https://gohugo.io/) - 静的サイトジェネレーター
- [Ananke](https://github.com/theNewDynamic/gohugo-theme-ananke) - Hugoテーマ
- GitHub Pages - ホスティング
- GitHub Actions - 自動デプロイ

## ローカル開発

### 必要なもの

- Hugo Extended (v0.128.0以上推奨)
- Git

### セットアップ

```bash
# リポジトリのクローン
git clone https://github.com/KeitaOsaki/portfolio.git
cd portfolio

# サブモジュールの初期化
git submodule update --init --recursive

# 開発サーバーの起動（Hugo v0.128.0以上の場合）
hugo server
```

開発サーバーが起動したら、ブラウザで http://localhost:1313/portfolio/ にアクセスしてください。

## デプロイ

このサイトはGitHub Actionsを使用して自動的にGitHub Pagesにデプロイされます。

### 初回デプロイ手順

1. GitHubで新しいリポジトリ `portfolio` を作成
2. リポジトリの Settings > Pages で、Source を "GitHub Actions" に設定
3. 以下のコマンドでプッシュ:

```bash
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/KeitaOsaki/portfolio.git
git push -u origin main
```

4. GitHub Actionsが自動的にビルド・デプロイを実行します
5. デプロイ完了後、https://KeitaOsaki.github.io/portfolio/ でサイトが閲覧できます

## コンテンツの追加

### 新しいブログ記事

```bash
hugo new content/blog/post-title.md
```

### 新しいプロダクト紹介

```bash
hugo new content/products/project-name.md
```

## ライセンス

このプロジェクトはMITライセンスの下で公開されています。
