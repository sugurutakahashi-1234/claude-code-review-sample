# Claude Code Review Sample

Claude Code を使った GitHub Actions による自動コードレビューのサンプルリポジトリです。

## 概要

Pull Request が作成・更新されると、Claude Code が自動でコードレビューを行い、フィードバックをコメントとして投稿します。

## 機能

- PR 作成時の自動コードレビュー
- PR 更新時（ドラフト解除、再オープン）のレビュー再実行
- `@claude` メンションでの対話（PR・Issue）
- PR コード行へのコメントでの `@claude` 対応
- PR レビュー（Approve/Request changes/Comment）での `@claude` 対応
- 日本語でのレビューコメント
- リアルタイム進捗表示

## ワークフロー構成

| ファイル | 用途 |
|---------|------|
| `claude-code-review.yml` | PR の自動レビュー + PR 全体へのコメント `@claude` |
| `claude.yml` | Issue + PR コード行コメント + PR レビュー `@claude` |

## セットアップ

### 1. ワークフローファイルの配置

`.github/workflows/` 配下にワークフローファイルを配置します。

### 2. OAuth トークンの取得

Claude Code 内でスラッシュコマンドを実行してトークンを取得します：

1. Claude Code を起動
2. `/install-github-app` と入力して実行

対話形式で設定が進み、GitHub App のインストールと OAuth トークンの取得が完了します。

> **Note**: CLI から `claude /install-github-app` で実行するよりも、Claude Code 内から実行する方が安定して動作します。

### 3. GitHub Secrets への登録

取得したトークンを GitHub リポジトリの Secrets に登録します：

1. リポジトリの Settings → Secrets and variables → Actions
2. New repository secret をクリック
3. Name: `CLAUDE_CODE_OAUTH_TOKEN`
4. Value: 取得したトークンを貼り付け

詳細は [Claude Code Action のドキュメント](https://github.com/anthropics/claude-code-action#setup) を参照してください。

## 使い方

### 自動レビュー

PR を作成すると自動でレビューが実行されます。

### @claude メンション

以下の場所で `@claude` をメンションすると Claude が応答します：

- **PR 全体へのコメント**: 詳細なレビューを再実行
- **PR コード行へのコメント**: 指定したコードについて回答
- **PR レビュー**: レビュー内容に対して回答
- **Issue**: Issue の内容について回答

例：
```
@claude このコードのパフォーマンスを改善できますか？
```

## 参考リンク

- [Claude Code GitHub Action](https://github.com/anthropics/claude-code-action)
- [Claude Code ドキュメント](https://docs.anthropic.com/claude-code)

## ライセンス

MIT
