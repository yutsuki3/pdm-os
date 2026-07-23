# プロンプト定義: decompose-tasks

対象エージェント: [Specification Agent](../docs/agents/specification-agent.md) / [Orchestrator](../docs/agents/orchestrator.md)

## 目的

承認済み仕様書を、デザイン・実装それぞれのJiraタスク候補へ分解する。

## 入力

- 承認済み仕様書 (`status: approved`、[schemas/specification.schema.yaml](../schemas/specification.schema.yaml))

## 手順

1. 仕様書の `functional_requirements` と `wireflow_ref` を単位として、デザインタスク（画面・フロー単位）と実装タスク（機能・API単位）の候補を洗い出す。
2. タスクの粒度は、原則1機能要件につき1タスク以上とするが、明確な粒度基準は現時点でTBD。迷う場合は細かく分割し、統合はレビュー時に人間が行う前提とする。
3. 各タスク候補を [templates/jira-task.md](../templates/jira-task.md) 形式で記述し、Jira登録前に一意な `draft_id` を付与する。`draft_id` は英数字で始め、英数字・ハイフン・アンダースコア・ドットだけを使用し、同一の出力リスト内で重複させない。各受け入れ条件には、`source_type` / `source_ref` / `item_ref` の組で根拠を記載する。仕様書要件は `specification` / 仕様書ID / `FR-001` 等、画面は `wireflow` / ワイヤーフロー参照 / `S2` 等とする。
4. タスク間の依存関係（例: デザイン完了後に実装着手）が明らかな場合は「依存する他タスク」に記載する。草稿段階では `jira_task_draft` と対象の `draft_id` を、登録後は `jira_issue` とJira課題キーを用いる。
5. 見積り・アサイン・ラベル等、Jira運用固有の項目はTBDのまま出力し、埋めない。

## 出力形式

`templates/jira-task.md` を埋めたタスク候補のリスト。Jiraへの登録は本プロンプトの範囲外（人間が確認・実施）。

## 禁止事項

- 未確定のプロジェクトキー・課題タイプ・カスタムフィールド値を推測して埋めること。
- タスク候補をJiraに直接登録すること（登録は人間が行う）。

## 未確定事項

- タスク分解の粒度基準。
- Jiraプロジェクトキー・課題タイプ体系・必須フィールド。
