---
name: build-status
description: GitHub Actionsの最新ビルド状況を確認し、結果を報告する
---

GitHub Actionsのビルド状況を確認します。

## 手順

1. `gh run list --limit 5` で最近のワークフロー実行を一覧表示
2. 最新の実行について `gh run view <run-id>` で詳細を確認
3. 失敗している場合は `gh run view <run-id> --log-failed` でエラーログを取得
4. 結果をユーザーに以下の形式で報告:
   - ビルド状態（成功/失敗/実行中）
   - 対象ブランチとコミット
   - 失敗時：エラー内容と推定原因
   - 各シールド（left/right/settings_reset）の個別結果
