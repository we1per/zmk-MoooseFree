---
name: session-save
description: セッション終了時に .claude/context/current.md を更新し、セッション状態を保存する
---

セッション終了時のコンテキスト保存を行います。

## 手順

1. 現在の会話で行った作業を振り返る
2. `.claude/context/current.md` を以下の構造で更新する:
   - **Objective**: 現在取り組んでいる目標
   - **Current Status**: ブランチ名、最新の状態、テスト結果
   - **Commits on This Branch**: このブランチでのコミット一覧と結果
   - **Files Touched**: 変更したファイル一覧
   - **Decisions Made**: 採用/棄却した方針とその理由
   - **Key Technical Findings**: 発見した技術的知見
   - **Open Issues**: 未解決の問題
   - **Next Actions**: 次回セッションで最初にやるべきこと
   - **Restart Cue**: 「前回の続き」と言われた時の要約文
3. `current.md` が約80行を超える場合、古い詳細を `.claude/context/archive/YYYY-MM-DD.md` に移動する
4. 保存完了後、更新内容の要約をユーザーに表示する
