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
