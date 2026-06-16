# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 作業スタイル

ユーザーは環境構築が得意でないため、Claude はアドバイザーとして手順・コマンドを提示し、ユーザーが自分で手打ちして進める。Claude が直接コマンドを実行することは原則しない。

## 目的

GitHub Pages を使ったシンプルな個人ブログ。Markdown で記事を書いて `main` ブランチに push すると、GitHub Actions が Hugo を実行して自動デプロイされる。

## リポジトリ情報

- GitHub: https://github.com/Tobiuo1022/Tobiuo-Blog
- 公開 URL: https://tobiuo1022.github.io/Tobiuo-Blog/
- ローカルパス: `/home/tobiuo/park/hugo`

## 技術的な決定事項

- **Hugo テーマ**: PaperMod（git submodule で管理、`.gitmodules` 必須）
- **Hugo の実行環境**: GitHub Actions のみ（ローカルには Hugo をインストールしない）
  - ワークフローで `hugo_extended_0.147.9` を直接ダウンロードしてインストール
- **デプロイ**: GitHub Actions → GitHub Pages（Actions ソース方式）
- **記事フォーマット**: Markdown（`content/posts/<記事名>/index.md`）
- **CLAUDE.md**: `.gitignore` に追加済み（ローカルのみ、push しない）

## セットアップ状況（完了）

- [x] git init
- [x] Hugo サイト生成（Docker 経由）
- [x] PaperMod テーマ追加（git submodule）
- [x] `hugo.toml` 設定
- [x] `.github/workflows/deploy.yml` 作成
- [x] `.gitignore` 作成
- [x] サンプル記事作成（`content/posts/hello-world/index.md`）
- [x] GitHub リポジトリに push
- [x] GitHub Pages の Source を「GitHub Actions」に設定
- [x] 公開確認済み

## 記事の書き方

`content/posts/<記事名>/index.md` を作成して push するだけ。

```markdown
+++
date = '2026-06-16T00:00:00Z'
draft = false
title = '記事タイトル'
tags = ['タグ']
+++

本文をここに書く。
```

`draft = false` にしないと公開されない。

## GitHub Actions デプロイフロー

`main` への push をトリガーに：
1. `actions/checkout`（submodules: true で PaperMod も取得）
2. `hugo_extended_0.147.9` をインストール
3. `hugo --minify` でビルド
4. `actions/deploy-pages` で GitHub Pages へデプロイ
