# Claude Code Review Sample

Claude Code を使った GitHub Actions による自動コードレビューのサンプルリポジトリです。

## 概要

Pull Request が作成・更新されると、Claude Code が自動でコードレビューを行い、フィードバックをコメントとして投稿します。

## 機能

- PR 作成時の自動コードレビュー
- PR 更新時（追加コミット、ドラフト解除、再オープン）のレビュー再実行
- `@claude` メンションでの対話
- Issue での `@claude` メンションにも対応
- 日本語でのレビューコメント

## ワークフロー構成

| ファイル | 用途 |
|---------|------|
| `claude-code-review.yml` | PR の自動レビュー |
| `claude.yml` | `@claude` メンションへの応答 |

## セットアップ

1. `.github/workflows/` 配下にワークフローファイルを配置
2. OAuth トークンを取得（詳細は [Claude Code Action のドキュメント](https://github.com/anthropics/claude-code-action#setup) を参照）
3. GitHub Secrets に `CLAUDE_CODE_OAUTH_TOKEN` を登録

## 参考リンク

- [Claude Code GitHub Action](https://github.com/anthropics/claude-code-action)
- [Claude Code ドキュメント](https://docs.anthropic.com/claude-code)

## ライセンス

MIT
