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

### 1. ワークフローファイルの配置

`.github/workflows/` 配下にワークフローファイルを配置します。

### 2. OAuth トークンの取得

Claude Code CLI を使用してトークンを取得します：

```bash
# Claude Code がインストールされていない場合
npm install -g @anthropic-ai/claude-code

# GitHub App をインストールしてトークンを取得
claude /install-github-app
```

対話形式で設定が進み、GitHub App のインストールと OAuth トークンの取得が完了します。

### 3. GitHub Secrets への登録

取得したトークンを GitHub リポジトリの Secrets に登録します：

1. リポジトリの Settings → Secrets and variables → Actions
2. New repository secret をクリック
3. Name: `CLAUDE_CODE_OAUTH_TOKEN`
4. Value: 取得したトークンを貼り付け

詳細は [Claude Code Action のドキュメント](https://github.com/anthropics/claude-code-action#setup) を参照してください。

## 参考リンク

- [Claude Code GitHub Action](https://github.com/anthropics/claude-code-action)
- [Claude Code ドキュメント](https://docs.anthropic.com/claude-code)

## ライセンス

MIT
