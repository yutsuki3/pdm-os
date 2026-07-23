<!--
テンプレート: QA依頼
対応スキーマ: schemas/acceptance-report.schema.yaml (受領情報を参照)
関連ワークフロー: docs/workflows/qa-request.md
送付先・送付方法・合否基準はTBD。
-->

# QA依頼: {{タイトル}}

- 対応Work Item: {{Work Item ID}}
- 対応仕様書: {{Specification ID}}
- 依頼日: {{YYYY-MM-DD}}
- 依頼者 (PdM/PO): {{氏名}}

## 対象機能の概要

{{何を検証してほしいか}}

## 関連リンク

- 仕様書 (Notion): {{URL}}
- Jiraタスク: {{キー一覧}}
- 実装 (GitHub PR): {{URL一覧}}
- 受領レポート: {{schemas/acceptance-report.schema.yaml 準拠のレポートへの参照}}

## テスト対象範囲

- 対象: {{機能・画面}}
- 対象外: {{明示的に除外するもの}}

## 検証環境

{{TBD — ステージング等の環境情報。命名規則未確定}}

## 合否基準 (Entry / Exit Criteria)

- Entry: {{TBD}}
- Exit: {{TBD}}

## リスク・注意点

{{既知の懸念事項、優先的に見てほしい観点}}

## 送付先

{{TBD — QAチームへの送付方法（専用Jiraチケット/フォーム等）未確定}}
