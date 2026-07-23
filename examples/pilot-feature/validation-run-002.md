<!--
これは架空のサンプルに基づく検証実施記録です。実在の組織・製品・意思決定とは関係ありません。
templates/validation-run.md を実際に埋めた例。schemas/validation-run.schema.yaml 準拠。
prompts/run-validation-dry-run.md に従って実施。
前回の検証記録: examples/pilot-feature/dry-run-result.md（第1部・第2部）
今回は、Codexレビューで追加された draft_id / trace_refs / dependency_refs（jira-task.schema.yaml）と
validation-run 形式そのものを使って、同じダミーパイプラインを再実行した。
-->

# 検証実施記録: VR-DRYRUN-002

- モード: dry_run
- 目的: Codexレビューで追加されたJiraタスク草稿の新形式（`draft_id` / `trace_refs` / 構造化された `dependency_refs`）と、`validation-run` 形式そのものが機能するかを、同一のダミーパイプライン（examples/pilot-feature、通知設定のカスタマイズ機能）で再確認する。TBD-058〜060の解消策を実際に成果物へ適用して確認する。
- 開始日時: 2026-07-23T00:00:00+09:00
- 完了日時: 2026-07-23T00:00:00+09:00（Jiraタスク草稿〜リリースノートまでの草稿作成を完了。実登録・実送付・実公開は未実施）

## 対象成果物

| 種別 | 参照 |
|---|---|
| requirement | [input.md](input.md) |
| knowledge_pack | [knowledge-pack.yaml](knowledge-pack.yaml) |
| specification | [specification.md](specification.md)（SPEC-SAMPLE-001） |
| wireflow | [wireflow.md](wireflow.md) |
| jira_task_draft | [jira-tasks/JT-SAMPLE-001-design.md](jira-tasks/JT-SAMPLE-001-design.md) |
| jira_task_draft | [jira-tasks/JT-SAMPLE-002-fr001-toggle-ui.md](jira-tasks/JT-SAMPLE-002-fr001-toggle-ui.md) |
| jira_task_draft | [jira-tasks/JT-SAMPLE-003-fr002-immediate-reflection.md](jira-tasks/JT-SAMPLE-003-fr002-immediate-reflection.md) |
| jira_task_draft | [jira-tasks/JT-SAMPLE-004-fr003-default-inheritance.md](jira-tasks/JT-SAMPLE-004-fr003-default-inheritance.md) |
| acceptance_report | [acceptance-report.md](acceptance-report.md) |
| qa_request | [qa-request.md](qa-request.md) |
| qa_result | [qa-result.yaml](qa-result.yaml) |
| release_note | [release-note.md](release-note.md) |

## テスト用の仮定

各仮定は実際の状態を変更しない。実際の記録と異なる場合は、その記録を必ず併記する。

| 仮定ID | 内容 | 適用対象 | 実際の記録への参照 |
|---|---|---|---|
| ASSUMPTION-001 | 検証に限り、仕様書 SPEC-SAMPLE-001 を仮承認として扱い、Jiraタスク草稿の作成を進める | jira-tasks/JT-SAMPLE-001〜004 | [specification.md](specification.md) の実際のステータスは `draft`（未承認） |
| ASSUMPTION-002 | 検証に限り、受領レポートの判断を仮で `accepted` として扱い、QA依頼作成に進める | qa-request.md | [acceptance-report.md](acceptance-report.md) の実際の `decision` は `pending`（FR-002は `unclear`、FR-003は `partially_met`） |
| ASSUMPTION-003 | 検証に限り、QA結果を仮で `passed` として扱い、リリースノート作成に進める | qa-result.yaml, release-note.md | QA結果の正本システム自体が未割当（[TBD-050](../../docs/decisions/tbd-register.md)）のため、`qa-result.yaml` は実施記録ではなくダミーであることをファイル冒頭に明記済み |

## 検証結果・発見事項

- **TBD-058（デザインタスクのワイヤーフロー画面ID参照）**: `trace_refs` に `source_type: wireflow` を指定することで、JT-SAMPLE-001 の受け入れ条件が `wireflow.md` の画面ID（S2）を自然に参照できることを確認した。仕様書要件（`source_type: specification`）と混在させても表現上の矛盾は生じない。
- **TBD-059（草稿間の依存関係参照）**: `draft_id`（例: `JT-SAMPLE-002`）を各草稿に付与し、`dependency_refs` を `{target_type: jira_task_draft, target_ref: <draft_id>}` の形で記載することで、Jira未登録の段階でも依存関係を一意に表現できることを確認した（JT-SAMPLE-002/003/004 → JT-SAMPLE-001 or 002）。登録後に `jira_issue` + 課題キーへ切り替える運用は、今回は実施できていない（Jira未接続のため）。
- **TBD-060（一部工程だけを仮定する検証の型）**: 本記録（`validation-run`）自体がこの課題への解となっている。上記の仮定3件はいずれも「実際の記録は変更せず、何を仮定したかを明示する」形で表現でき、[dry-run-result.md](dry-run-result.md) 第2部で各成果物に手動の注記を分散させていたやり方より、一箇所に集約されて追跡しやすくなった。
- **新たな所見（TBD-061関連）**: 本記録も含め、すべての成果物はMarkdownの人間可読テキストであり、`validation-run.schema.yaml` 等のSchemaに対する機械的な検証（必須項目の充足チェックなど）は今回も目視で行った。TBD-061（Markdown成果物とSchemaの機械検証方法）は未解決のまま。
- **新たな所見**: `draft_id` の採番規則自体（例えば `JT-SAMPLE-00X` のような連番の一意性をどう保証するか）はまだ `TBD` のままであり、`jira-task.schema.yaml` のコメントどおり未確定事項として残っている。

## 人間の確認が必要な事項

- [jira-tasks/](jira-tasks/) 配下4件の `trace_refs` / `dependency_refs` の使い方が、実際のJira運用（画面IDやワイヤーフロー参照をJira側でどう表現するか）と整合するかは、実案件でのみ確認できる。
- ASSUMPTION-001〜003はいずれもテスト用であり、実際の承認・受領・QA合否が確定するまで、対応する下流工程（Jira登録・QA送付・公開）を進めてはならない。
- TBD-058〜060は「定義の追加」までは完了したとみなせるが、実案件での運用検証（実際のJira・QAプロセスでの使用）はまだ行われていない。ステータスは「実案件未検証」として区別する（[tbd-register.md](../../docs/decisions/tbd-register.md) 参照）。
