# ワークフロー: 仕様書 → Jiraタスク分解

## 目的

承認済みの仕様書を、デザイン・実装それぞれのJiraタスクへ分解する。

## 関係者・エージェント

- Specification Agent / Orchestrator: タスク分解の草稿作成
- PdM/PO: タスク分解内容の確認・Jiraへの登録可否判断

## 手順

1. **前提確認**
   Work Itemが `spec_approved` 状態であることを確認する。

2. **タスク分解の草稿作成**
   [prompts/decompose-tasks.md](../../prompts/decompose-tasks.md) に従い、仕様書のセクション（機能要件・非機能要件・画面単位など）ごとに、デザインタスク・実装タスク候補を洗い出す。
   各タスクは [templates/jira-task.md](../../templates/jira-task.md) 形式で草稿化する。

3. **タスク粒度・依存関係の確認**
   PdM/POがタスク分解案をレビューする。分解の粒度基準（1画面1タスクか、機能単位かなど）はTBD。

4. **Jiraへの登録**
   承認された分解案をJiraに登録する。プロジェクトキー・課題タイプ・必須カスタムフィールドはTBD ([source-of-truth.md](../architecture/source-of-truth.md))。
   登録後、各Jiraタスクを仕様書（Notion）・Work Itemと相互リンクする。

5. **状態遷移**
   Work Itemを `jira_tasks_created` に遷移し、以降の進捗はJira側のステータスを正とする。

## 入力/出力まとめ

| ステップ | 入力 | 出力 |
|---|---|---|
| タスク分解草稿 | 承認済み仕様書 | `templates/jira-task.md` を埋めたタスク案リスト |
| Jira登録 | 承認されたタスク案 | Jira課題 (デザイン/実装) + 仕様書へのリンク |

## 未確定事項

- Jiraプロジェクトキー・課題タイプ体系・必須フィールド
- タスク分解の粒度基準
- 見積り（ストーリーポイント等）を誰が・どの段階で入れるか
- デザインタスクと実装タスクの依存関係の表現方法（Jira上のリンク種別）
