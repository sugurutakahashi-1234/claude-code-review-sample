# Claude Code Review Sample

[![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=flat&logo=githubactions&logoColor=white)](https://github.com/features/actions)
[![Claude](https://img.shields.io/badge/Powered%20by-Claude-orange?style=flat)](https://www.anthropic.com/claude)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)

Claude Code を使った GitHub Actions による自動コードレビューのサンプルリポジトリです。

## 概要

Pull Request が作成・更新されると、Claude Code が自動でコードレビューを行い、フィードバックをコメントとして投稿します。また、`@claude` メンションを使って PR や Issue 上で Claude と対話することもできます。

## 機能

| 機能 | 説明 |
|------|------|
| 自動コードレビュー | PR 作成・更新時に自動でレビューを実行 |
| `@claude` メンション | PR・Issue で Claude に質問・依頼が可能 |
| コード行へのコメント対応 | 特定のコード行に対して `@claude` で回答 |
| PR レビュー対応 | Approve / Request changes / Comment 時の `@claude` に対応 |
| 日本語サポート | レビューコメントは日本語で投稿 |
| リアルタイム進捗表示 | 処理中のスピナー表示で進捗を確認可能 |

## ワークフロー構成

| ファイル | 用途 |
|---------|------|
| `claude-code-review.yml` | PR の自動レビュー・PR 全体へのコメントで `@claude` に対応 |
| `claude.yml` | Issue・PR コード行コメント・PR レビューで `@claude` に対応 |

## セットアップ

### 1. ワークフローファイルの配置

`.github/workflows/` 配下にワークフローファイルを配置します。

### 2. OAuth トークンの取得

Claude Code 内でスラッシュコマンドを実行してトークンを取得します：

1. Claude Code を起動
2. `/install-github-app` と入力して実行

対話形式で設定が進み、GitHub App のインストールと OAuth トークンの取得が完了します。

> [!NOTE]
> CLI から `claude /install-github-app` で実行するよりも、Claude Code 内から実行する方が安定して動作します。

### 3. GitHub Secrets への登録

取得したトークンを GitHub リポジトリの Secrets に登録します：

1. リポジトリの **Settings** → **Secrets and variables** → **Actions**
2. **New repository secret** をクリック
3. **Name**: `CLAUDE_CODE_OAUTH_TOKEN`
4. **Value**: 取得したトークンを貼り付け

詳細は [Claude Code Action のドキュメント](https://github.com/anthropics/claude-code-action#setup) を参照してください。

## 使い方

### 自動レビュー

PR を作成すると自動でレビューが実行されます。ドラフト解除・再オープン時にも再実行されます。

### @claude メンション

以下の場所で `@claude` をメンションすると Claude が応答します：

| 場所 | 動作 |
|------|------|
| PR 全体へのコメント | 詳細なレビューを再実行 |
| PR コード行へのコメント | 指定したコードについて回答 |
| PR レビュー | レビュー内容に対して回答 |
| Issue | Issue の内容について回答・実装 |

**使用例：**

```
@claude このコードのパフォーマンスを改善できますか？
```

```
@claude このバグの原因を調べて修正してください
```

## 参考リンク

- [Claude Code GitHub Action](https://github.com/anthropics/claude-code-action)
- [Claude Code ドキュメント](https://docs.anthropic.com/claude-code)
- [Claude Code Action FAQ](https://github.com/anthropics/claude-code-action/blob/main/docs/faq.md)

## ライセンス

MIT
