# プロンプト定義: request-codex-review

対象エージェント: Codex（Schema・ファイル構造・文書間の整合性のレビュー担当。[docs/agents/ai-tool-roles.md](../docs/agents/ai-tool-roles.md) 参照）

## 目的

Claude Codeが実施したパイロットのダミーデータ検証結果をCodexにレビューさせ、Schema・テンプレート・文書間の整合性を確認・具体化する。同一ファイルを繰り返しのレビュー依頼に使い回す。中身は毎回の状況に合わせて更新し、[レビュー履歴](#レビュー履歴)に前回までの経緯を残す。

## 前提（第2回時点）

- 実案件・正本システムへの検索許可がまだ無いため、実データでのパイロットは未実施。
- 第1回レビュー（Round 1）でCodexが `jira-task.schema.yaml`（`draft_id` / `trace_refs` / 構造化された `dependency_refs`）と `validation-run.schema.yaml` / [run-validation-dry-run.md](run-validation-dry-run.md) を追加した。
- Claude Codeがこれらの新形式を使って同じダミーパイプラインを再実行し、[examples/pilot-feature/validation-run-002.md](../examples/pilot-feature/validation-run-002.md) として記録した。Jiraタスク草稿4件（`examples/pilot-feature/jira-tasks/*.md`）も新形式に更新済み。
- [tbd-register.md](../docs/decisions/tbd-register.md) のTBD-058〜060は、ダミーデータでの機能確認が完了した段階として `実案件未検証` ステータスに更新した。TBD-061（Markdown成果物とSchemaの機械検証方法）は未着手のまま。

## Codexへの実行プロンプト

```text
PdM OS設計リポジトリ（pdm-os）で、Claude Codeが実施したパイロットのダミーデータ検証結果（2回目）をレビューしてください。

## 背景
- このリポジトリは設計フェーズで、Claude Codeが業務フロー構造化・状態遷移設計・成果物整理・文書とテンプレートの初期案作成を担当し、Codexが後続でSchema・ファイル構造・文書間の整合性をレビュー・具体化する分担になっています（docs/agents/ai-tool-roles.md 参照）。
- 前回のレビュー（Round 1）で、あなた（Codex）は jira-task.schema.yaml に draft_id / trace_refs / 構造化された dependency_refs を追加し、validation-run.schema.yaml / templates/validation-run.md / prompts/run-validation-dry-run.md を新設しました。
- Claude Codeはこれらの新形式を使って、架空サンプル(examples/pilot-feature、通知設定のカスタマイズ機能)で同じダミーパイプラインを再実行しました。

## まず読んでほしいもの
1. docs/workflows/pilot-core-flow.md の「実施履歴」セクション（今回追加分を含む）
2. examples/pilot-feature/validation-run-002.md（新形式での再実行記録。前回の examples/pilot-feature/dry-run-result.md も経緯として参照可）
3. docs/decisions/tbd-register.md のTBD-058〜061（ステータスが `実案件未検証` に更新された経緯とTBD-061）

## レビュー対象の成果物一式
- examples/pilot-feature/jira-tasks/*.md（4件、新形式: draft_id, trace_refs, dependency_refs）
- examples/pilot-feature/validation-run-002.md（validation-run.schema.yaml への準拠）
- examples/pilot-feature/qa-request.md, qa-result.yaml（validation-run-002.md への参照を追記した箇所）

## 依頼内容
1. 更新後のjira-task.schema.yaml・validation-run.schema.yamlに対して、上記成果物が必須項目・型を満たしているか確認する。
2. draft_id・trace_refs・dependency_refsの使い方が、スキーマの意図（草稿段階と登録後の参照を区別する）どおりになっているか確認する。
3. TBD-058〜060を`実案件未検証`のまま維持してよいか、それとも定義レベルでも追加の不備が残っているかを判定する。
4. TBD-059の残課題である「draft_idの採番規則」について、Codexとして具体化できる範囲があれば提案する（業務ルール確定は行わない）。
5. TBD-061（Markdown成果物とSchemaの機械検証方法）について、方針の提案があれば行う。まだ未着手のままでもよい。
6. 出力ファイル(examples/pilot-feature/以下)は、成果物契約(artifact-contracts.md)に照らして不足がなければ変更不要。修正が必要なのはschemas/templates/promptsなど、リポジトリ全体で再利用される定義側に限定する。
7. 業務ルール（承認者、優先度基準、Jira運用ルール等）を推測して確定しないこと。事実・仮定・提案・決定の区別(AGENTS.md参照)を維持し、決定を下す場合は必ずADRとして記録すること。

## 出力してほしいもの
- レビュー結果のサマリ（各schemaの適合状況、TBD-058〜061それぞれへの見解）
- 必要なschemas/templates/promptsの修正（あれば）
- tbd-register.mdの更新（ステータス変更・新規TBD追加。変更理由を明記）
- 未解決のまま残すべき事項の一覧
```

## 禁止事項

- 業務ルール（承認者、優先度基準、Jiraプロジェクト構成等）を推測して確定すること。
- `examples/pilot-feature` の出力ファイルを、schemas/templatesの不備によらない理由で書き換えること（内容の良し悪しではなく契約適合性のレビューに限定する）。
- レビュー結果を人間の承認なしに「決定」として記録すること（ADR化する場合もステータスは提案段階から開始する）。

## レビュー履歴

- Round 1（2026-07-23）: TBD-058〜060の発見を受けてレビュー依頼。Codexが jira-task.schema.yaml（draft_id/trace_refs/dependency_refs）と validation-run 一式（schema/template/prompt）を追加。TBD-061を新規発見。
- Round 2（2026-07-23）: Round 1の修正を使ってダミーパイプラインを再実行した結果（validation-run-002.md）のレビューを依頼。TBD-058〜060の「実案件未検証」ステータスの妥当性確認、TBD-059の採番規則・TBD-061への提案を依頼中。
