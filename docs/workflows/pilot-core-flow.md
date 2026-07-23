# パイロット: 要求・要望からJiraタスク草稿まで

## 目的

【提案】実装・外部システムへの書き込みを開始する前に、1件の低リスクな実案件を用いて、`requested` から `spec_review` のレビュー準備、およびJiraタスク**草稿**までの成果物契約を検証する。

このパイロットは、PdM/POの承認やJira・Notionへの正式登録を自動化しない。QA・リリース工程は、QA結果や公開済みリリースノートの正本が未決定のため対象外とする。

実案件または正本システムへのアクセスがない場合は、[run-validation-dry-run.md](../../prompts/run-validation-dry-run.md) に従い、検証実施記録を作成してメカニクスのみを確認する。ドライランの仮定は実際の状態を変更しない。

## 対象の選定条件

対象案件はPdM/POが選定する。次を満たすことが望ましい。

- 既存の現行仕様（Notion）と関連する過去資料が存在する、または「存在しない」と確認できる。
- 機密情報をこのリポジトリに複製せず、外部正本へのURL/ID参照だけで成果物をレビューできる。
- リリース期限・承認を急がず、草稿レビューの時間を確保できる。

選定者、案件名、優先度、実施期限は業務判断であり `TBD`。本ドキュメントでは決めない。

## 実案件パイロットの準備メモ

【提案】初回の実案件パイロットは、QA・リリースまで拡大せず、要求・要望からJiraタスク草稿までを対象にする。以下は開始時にPdM/POとClaude Codeが確認する作業メモであり、承認者・優先度・Jira運用等の業務ルールを決めるものではない。

### PdM/POが開始前に明示するもの

- 対象案件のWork Item ID
- 要求原文、または要求原文を辿れる正本への参照
- 検索を許可する正本システムと検索範囲
- 仕様書草稿をレビューする人間と、確認・承認を依頼する方法（役職・基準が未確定なら `TBD` のまま明示）

### 実施の順序

| 段階 | 人間が行うこと | Claude Codeが行うこと | 次へ進むための確認 |
|---|---|---|---|
| 1. 対象・検索範囲の確定 | 上記の開始情報を渡す | 許可範囲と不足情報を確認する | 要求原文、Work Item ID、検索範囲が明確 |
| 2. 知識収集 | 必要に応じて検索結果を確認する | 現行仕様・過去資料を知識パックに整理し、重複・矛盾を記録する | 出所・正本URL/IDを辿れる |
| 3. 草稿作成 | 未解決論点をレビューする | 仕様書草稿、必要ならワイヤーフロー草稿を作成する | 要件ID、参照資料、TBDが明記される |
| 4. 仕様レビュー | 人間が草稿をレビューし、承認の要否を明示する | 修正依頼を草稿へ反映する。承認状態は確定しない | 人間が次の扱いを明示 |
| 5. タスク草稿 | 承認済み仕様書であることを明示する | Jiraタスク草稿を作成し、`draft_id`・根拠参照・依存関係を付与する | 草稿間の参照を辿れる |
| 6. Jira登録 | 人間が登録・相互リンクを実施する | 登録結果の参照整合性を確認する | Jira課題キーと仕様書・Work Itemの参照が揃う |
| 7. 振り返り | 実務上の不足・不要項目を判断する | 発見事項をTBD候補として整理する | 更新すべき設計事項が記録される |

### 初回の範囲外

- QA依頼、QA合否、リリース可否、公開は、このメモだけでは開始しない。既存の正本・承認・QA運用のTBDが解消または人間により明示されてから扱う。
- TBD-061（Markdown成果物の機械検証方式）は初回パイロットの開始条件ではない。初回は人間のレビューで検証し、同じ不備が繰り返される場合に方式を検討する。
- Claude Codeは、外部正本への書込み、承認、状態遷移の確定を行わない。実行時は [run-pilot-core-flow.md](../../prompts/run-pilot-core-flow.md) を使用する。

## 実施手順

1. PdM/POが要求原文の参照、Work Item ID、検索してよい正本の範囲をClaude Codeに渡す。
2. Claude Codeが [collect-knowledge.md](../../prompts/collect-knowledge.md) に従い、知識パックを草稿化する。出所不明・矛盾・未確認事項は推測せず記録する。
3. Claude Codeが [create-specification.md](../../prompts/create-specification.md) に従い、仕様書草稿と必要なワイヤーフロー草稿を作成する。
4. 人間が要件・仕様書草稿をレビューする。承認者・基準・正式反映方法は既存の `TBD` に従い、このパイロットで勝手に確定しない。
5. 人間が承認済み仕様書を明示した場合に限り、Claude Codeが [decompose-tasks.md](../../prompts/decompose-tasks.md) に従いJiraタスク草稿を作成する。
6. PdM/POが、成果物の完全性・参照の追跡可能性・TBDの妥当性を確認する。Jiraへの登録は人間が行う。

## 完了条件

以下を満たしたら、このパイロットの完了とする。

- 要求、知識パック、仕様書、必要ならワイヤーフロー、Jiraタスク草稿の参照関係を `work_item_id`、`specification_id`、要件ID、正本URL/IDで辿れる。
- 同一出所の転記を独立根拠として数えず、矛盾を検知した場合は出所とともに記録している。
- 人間の明示的な確認なしに、承認・Notion反映・Jira登録・状態確定をしていない。
- 新たに明らかになった業務ルールは、決定ではなく `TBD` として [tbd-register.md](../decisions/tbd-register.md) に追加されている。

## 評価・次の判断

PdM/POは、パイロット完了後に次を判断する。

- テンプレート・Schemaの不足または不要な項目
- 正本検索時の重複・矛盾記録が実務で十分か
- Jiraタスク粒度と依存関係表現が実務に合うか
- QA・リリース工程に進む前に解消すべきTBD

この評価結果をもとに更新する文書・Schemaは `TBD`。重要な方針変更はADRとして記録する。

## 実施履歴

- 【事実】2026-07-23: 実案件・正本アクセス許可がまだ無い状態で、[run-pilot-core-flow.md](../../prompts/run-pilot-core-flow.md) の手順・成果物契約が機能するかを検証するメカニクス確認ドライランを実施した。実データへは一切アクセスせず、既存の架空サンプル (`examples/pilot-feature`) を流用した。結果は [examples/pilot-feature/dry-run-result.md](../../examples/pilot-feature/dry-run-result.md) 第1部を参照。判明したギャップは [tbd-register.md](../decisions/tbd-register.md) のTBD-055〜057に追加。
- 【事実】2026-07-23: 同日、PdM/POの指示によりダミーデータでの検証範囲をパイプライン全体（Jiraタスク草稿〜リリースノート）に拡大した。「仕様書はテスト用に仮承認された」という明示的なテスト信号のもとで実施し、実際の承認・受領判断・送付・公開は一切行っていない。結果は [dry-run-result.md](../../examples/pilot-feature/dry-run-result.md) 第2部を参照。判明したギャップは [tbd-register.md](../decisions/tbd-register.md) のTBD-058〜060に追加。
- 【事実】2026-07-23: Codexレビュー Round 1。[prompts/request-codex-review.md](../../prompts/request-codex-review.md) に基づきレビューを行い、`jira-task.schema.yaml`（`draft_id` / `trace_refs` / 構造化された `dependency_refs`）と `validation-run.schema.yaml` / [run-validation-dry-run.md](../../prompts/run-validation-dry-run.md) を追加した。これを受け、同日中に新形式で同じダミーパイプラインを再実行した。結果は [validation-run-002.md](../../examples/pilot-feature/validation-run-002.md) を参照。TBD-058〜060はダミーデータ上での機能を確認済みとして、ステータスを `実案件未検証` に更新した（[tbd-register.md](../decisions/tbd-register.md) 参照）。
- 【事実】2026-07-23: Codexレビュー Round 2（完了）。`draft_id` の許容文字・一意性制約、`validation-run` の `actual_record_ref` 必須化を追加し、TBD-061にYAML front matter方式の提案（未実装）を追記した。PdM/POが結果を確認し、TBD-058〜060は「実案件未検証」のまま維持で妥当と判定、既存のダミー成果物は変更不要と確認した。TBD-061は方式未確定のまま `検討中` を維持する。次回のCodexレビュー（Round 3）は依頼内容未定のまま準備のみ行った（[request-codex-review.md](../../prompts/request-codex-review.md) レビュー履歴参照）。
- 実案件を用いた本番パイロットは未実施 (`TBD`)。対象案件・検索許可が人間から明示されるまで開始しない。
