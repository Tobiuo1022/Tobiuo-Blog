# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 作業スタイル

ユーザーは環境構築が得意でないため、Claude はアドバイザーとして手順・コマンドを提示し、ユーザーが自分で手打ちして進める。Claude が直接コマンドを実行することは原則しない。

## 目的

GitHub Pages を使ったシンプルな個人ブログの構築。Markdown で記事を書いて `main` ブランチに push すると、GitHub Actions が Hugo を実行して自動デプロイされる構成を目指している。

## リポジトリ情報

- GitHub: https://github.com/Tobiuo1022/Tobiuo-Blog
- 公開 URL: https://Tobiuo1022.github.io/Tobiuo-Blog/
- ローカルパス: `/home/tobiuo/park/hugo`

## 技術的な決定事項

- **Hugo テーマ**: PaperMod（git submodule で管理）
- **Hugo の実行環境**: Docker コンテナ内のみ（ホストに Hugo をインストールしない）
  - 使用イメージ: `hugomods/hugo:exts`（extended 版、SCSS 対応）
- **デプロイ**: GitHub Actions → GitHub Pages（Actions ソース方式）
- **記事フォーマット**: Markdown（`content/posts/` 以下）

## セットアップ状況

- [x] git init 済み（`/home/tobiuo/park/hugo`）
- [ ] `hugo new site .` 実行（Docker 経由）
- [ ] PaperMod テーマ追加（git submodule）
- [ ] `hugo.toml` 設定
- [ ] `.github/workflows/deploy.yml` 作成
- [ ] `Makefile` 作成（Docker ラッパーコマンド）
- [ ] `.gitignore` 作成
- [ ] サンプル記事作成
- [ ] GitHub リポジトリに push
- [ ] GitHub Pages の Source を「GitHub Actions」に設定

## ローカル開発（予定）

Hugo はホストにインストールせず、すべて Docker 経由で操作する予定。

```bash
make serve    # ローカルプレビュー (http://localhost:1313)
make new-post NAME=my-first-post  # 新規記事作成
make build    # 静的ファイル生成
```

## GitHub Actions デプロイフロー（予定）

`main` ブランチへの push をトリガーに：
1. `actions/checkout`（submodules: true）
2. Hugo でビルド（`--minify`）
3. `actions/deploy-pages` で GitHub Pages へデプロイ
