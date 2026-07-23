# 成果物契約（入力・出力・正本）

【提案】将来の実装でエージェント間の受け渡しを検証可能にするため、既存テンプレートとSchemaの対応、成果物の入力・出力、正本をこの表で一元化する。本表は承認者や業務基準を新たに決めるものではなく、未確定のものは `TBD` とする。

## 成果物一覧

| 成果物 | 作成者 | 主な入力 | 構造 | 正本 / 扱い | 次の利用者 |
|---|---|---|---|---|---|
| 要求・要望記録 | PdM/PO | ステークホルダーの発話・依頼 | [requirement.schema.yaml](../../schemas/requirement.schema.yaml) / [requirement.md](../../templates/requirement.md) | 原文の外部正本・保存先: `TBD`。リポジトリ内の例・草稿は正本でない | Knowledge Agent, Specification Agent |
| 知識パック | Knowledge Agent | 要件・検索クエリ・外部正本の検索結果 | [knowledge-item.schema.yaml](../../schemas/knowledge-item.schema.yaml) のリスト | 各アイテムの正本は `source_system` の参照先。知識パック自体は中間成果物 | Specification Agent, Acceptance Agent |
| 仕様書 | Specification Agent（草稿） | 要件、知識パック | [specification.schema.yaml](../../schemas/specification.schema.yaml) / [specification.md](../../templates/specification.md) | 承認後の正本はNotion。草稿は中間成果物 | PdM/PO、Specification Agent（タスク分解）、Acceptance Agent |
| ワイヤーフロー | Specification Agent（草稿） | 仕様書草稿 | [wireflow.schema.yaml](../../schemas/wireflow.schema.yaml) / [wireflow.md](../../templates/wireflow.md) | 正式ツール・正本・同期方法: `TBD` | 仕様書レビュー、Jiraタスク分解 |
| Jiraタスク草稿 | Specification Agent | 承認済み仕様書 | [jira-task.schema.yaml](../../schemas/jira-task.schema.yaml) / [jira-task.md](../../templates/jira-task.md) | 登録後のJira課題・状態の正本はJira。草稿は中間成果物 | PdM/PO、Jira |
| 受領レポート | Acceptance Agent（草稿） | 承認済み仕様書、GitHub実装、Drive受領原本 | [acceptance-report.schema.yaml](../../schemas/acceptance-report.schema.yaml) | GitHub/Google Driveへの参照に基づく判断材料。最終判断は人間 | PdM/PO、Release Agent |
| QA依頼 | Release Agent（草稿） | `accepted` のWork Item、受領レポート、関連参照 | [qa-request.schema.yaml](../../schemas/qa-request.schema.yaml) / [qa-request.md](../../templates/qa-request.md) | 送付先・送付記録の正本: `TBD` | PdM/PO、QAチーム |
| QA結果参照 | QAチーム（記録主体はTBD） | QA実施結果 | [qa-result.schema.yaml](../../schemas/qa-result.schema.yaml) | **QA結果の正本システムは未割当 (`TBD`)**。このSchemaは正式記録への参照のみを表す | Orchestrator、Release Agent |
| リリースノート | Release Agent（草稿） | `qa_passed` のWork Item群、仕様書、Jira、GitHub | [release-note.schema.yaml](../../schemas/release-note.schema.yaml) / [release-note.md](../../templates/release-note.md) | 公開先・アーカイブ先の正本: `TBD` | PdM/PO、公開先 |
| 検証実施記録 | パイロット実施者 | 対象成果物、テスト用の仮定 | [validation-run.schema.yaml](../../schemas/validation-run.schema.yaml) / [validation-run.md](../../templates/validation-run.md) | パイプラインの検証記録。業務上の承認・状態の正本ではない | PdM/PO、設計レビュー担当 |

## 横断ルール

- 成果物間の参照は、可能な限り `work_item_id`、`specification_id`、要件ID（`FR-001`等）と正本URL/IDで辿れるようにする。IDの採番規則は `TBD`。
- エージェントが出力するものは常に草稿または判断材料である。承認、送付、公開、状態の確定は人間の操作・記録を必要とする。
- 参照情報に矛盾または同一出所の転記がある場合は、[deduplication-policy.md](deduplication-policy.md) と `knowledge-item` の `origin` / `conflicts` に従う。推測で出所や解決結果を補わない。
- Work Itemは成果物本体ではなく、状態と成果物参照を束ねる制御単位である。実行時インスタンスの永続化は `TBD`。
- ドライランで置く仮定は、実際の記録への参照を併記し、検証実施記録に閉じ込める。仮定を実際の業務状態へ反映してはならない。

## 未確定事項

- QA結果の正本システム、結果記録の形式、QA不合格時の戻り先。
- 要求原文、ワイヤーフロー、QA依頼送付記録、リリースノート公開記録の正本・保存先。
- 成果物IDと要件IDの採番規則、状態遷移履歴の保管先。
