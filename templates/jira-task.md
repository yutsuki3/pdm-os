<!--
テンプレート: Jiraタスク草稿
関連ワークフロー: docs/workflows/spec-to-jira.md
対応スキーマ: schemas/jira-task.schema.yaml
1案件 (Work Item) = 1ストーリー、その配下に複数タスクを作る階層とする。
課題タイプはJira標準を使い、デザイン／実装の区別はラベルで表す。
プロジェクトキーの具体値・必須カスタムフィールドはTBD。
このテンプレートはJira登録前の草稿として使う。
-->

# Jiraタスク草稿: {{タイトル}}

- 草稿ID: {{例: JTD-001。同一の草稿リスト内で一意。英数字で始め、英数字・ハイフン・アンダースコア・ドットのみ。採番規則はTBD。Jira課題キーとは別}}
- 対応仕様書: {{Specification ID}}
- 課題タイプ: {{Jira標準の課題タイプ。案件全体は Story、個々の作業は Task}}
- ラベル: {{design / implementation のいずれか。デザインと実装の区別はラベルで表す}}
- 親ストーリー: {{この案件のストーリーの課題キー。未登録なら親Work Item IDを記載}}
- プロジェクトキー: {{TBD — 具体値は未確認}}

## 概要

{{このタスクで何を行うか}}

## 受け入れ条件 (Acceptance Criteria)

- [ ] {{条件1}}
  - 根拠: {{source_type: specification / wireflow / jira_task_draft / jira_issue}}, {{source_ref: 仕様書ID等}}, {{item_ref: FR-001 / S2等}}
- [ ] {{条件2}}

## 関連リンク

- 仕様書 (Notion): {{URL}}
- 親Work Item: {{Work Item ID}}
- 依存する他タスク: {{草稿段階は jira_task_draft + 草稿ID、登録後は jira_issue + Jira課題キー。なければ「なし」}}

## 見積り

{{TBD — 見積り単位 (ストーリーポイント/時間) とタイミングは未確定}}

## ラベル・コンポーネント

- 必須: design / implementation のいずれか（課題タイプでは区別しないため）
- その他のラベル・コンポーネント: {{TBD — Jira側の運用ルール次第}}

## 担当候補

{{TBD — アサインルールは本リポジトリのスコープ外/未確定}}
