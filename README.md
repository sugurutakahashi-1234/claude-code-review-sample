# Claude Code Review Sample

Claude Code を使った GitHub Actions による自動コードレビューのサンプルリポジトリです。

## 概要

Pull Request が作成・更新されると、Claude Code が自動でコードレビューを行い、フィードバックをコメントとして投稿します。

## 機能

- PR 作成時の自動コードレビュー
- PR 更新時のレビュー再実行（同じコメントを更新）
- ドラフト PR のスキップ
- リリース PR（develop → main）のスキップ

## セットアップ

### 1. リポジトリにワークフローをコピー

`.github/workflows/claude-code-review.yml` をリポジトリに配置します。

### 2. OAuth トークンの設定

#### 方法 A: 自動セットアップ（推奨）

```bash
claude /install-github-app
```

#### 方法 B: 手動セットアップ

1. トークンを取得
   ```bash
   claude setup-token
   ```

2. GitHub Secrets に登録
   - リポジトリの **Settings** → **Secrets and variables** → **Actions**
   - **New repository secret** をクリック
   - **Name**: `CLAUDE_CODE_OAUTH_TOKEN`
   - **Value**: 取得したトークン

## ワークフローの動作

| トリガー | 動作 |
|---------|------|
| PR 作成 (`opened`) | 自動レビュー実行 |
| PR 更新 (`synchronize`) | レビュー再実行（コメント更新） |
| ドラフト解除 (`ready_for_review`) | 自動レビュー実行 |

### スキップ条件

- ドラフト PR
- `develop` → `main` へのリリース PR

## カスタマイズ

### 特定のファイルのみレビュー

```yaml
on:
  pull_request:
    paths:
      - "src/**/*.ts"
      - "src/**/*.tsx"
```

### レビューの観点を変更

```yaml
prompt: |
  このPRをレビューして、以下の観点でフィードバックをお願いします：
  - コード品質とベストプラクティス
  - 潜在的なバグや問題
  - パフォーマンスの考慮
  - セキュリティの懸念
  - テストカバレッジ
```

### モデルを変更

```yaml
# Claude Opus 4 を使用
claude_args: --model claude-opus-4-20250514
```

### テストやリントを実行

```yaml
claude_args: --allowedTools "Bash(npm run test),Bash(npm run lint),Bash(npm run typecheck)"
```

### 特定の著者のみレビュー

```yaml
if: |
  github.event.pull_request.draft == false &&
  github.event.pull_request.author_association == 'FIRST_TIME_CONTRIBUTOR'
```

## 認証方法

| 方法 | 設定 |
|------|------|
| OAuth トークン | `claude_code_oauth_token: ${{ secrets.CLAUDE_CODE_OAUTH_TOKEN }}` |
| API キー | `anthropic_api_key: ${{ secrets.ANTHROPIC_API_KEY }}` |

## 参考リンク

- [Claude Code GitHub Action](https://github.com/anthropics/claude-code-action)
- [Claude Code ドキュメント](https://docs.anthropic.com/claude-code)

## ライセンス

MIT
