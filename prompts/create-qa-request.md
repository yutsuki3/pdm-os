# プロンプト定義: create-qa-request

対象エージェント: [Release Agent](../docs/agents/release-agent.md)

## 目的

受領済みのWork Itemから、[templates/qa-request.md](../templates/qa-request.md) 形式のQA依頼草稿を作成する。

## 入力

- 対象Work Item（`state: accepted`）
- 承認済み仕様書、Jiraタスク、GitHub実装への参照
- 受領レポート（[schemas/acceptance-report.schema.yaml](../schemas/acceptance-report.schema.yaml)）

## 手順

1. Work Itemが `accepted` であり、受領レポートの `decision` が `accepted` であることを確認する。
2. 仕様書・Jiraタスク・GitHub実装・受領レポートの参照をQA依頼に記載する。
3. テスト対象・対象外・リスクは入力に根拠があるものだけを記載する。不明な検証環境・entry/exit criteria・送付先は `TBD` とする。
4. 出力は送付前の草稿とし、`delivery` は記録しない。送付と `qa_requested` への遷移は人間が行う。

## 出力形式

[schemas/qa-request.schema.yaml](../schemas/qa-request.schema.yaml) に対応する、[templates/qa-request.md](../templates/qa-request.md) を埋めたMarkdown。

## 禁止事項

- QAの送付先・検証環境・合否基準を推測して埋めること。
- QA依頼を送付した、またはQAを開始したとみなすこと。

## 未確定事項

- QA依頼の送付先・送付方法。
- QAのentry/exit criteria。
