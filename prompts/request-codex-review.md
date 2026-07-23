# プロンプト定義: request-codex-review

対象エージェント: Codex（Schema・ファイル構造・文書間の整合性のレビュー担当。[docs/agents/ai-tool-roles.md](../docs/agents/ai-tool-roles.md) 参照）

## 目的

Claude Codeが実施したパイロットのダミーデータ検証結果をCodexにレビューさせ、Schema・テンプレート・文書間の整合性を確認・具体化する。同一ファイルを繰り返しのレビュー依頼に使い回す。中身は毎回の状況に合わせて更新し、[レビュー履歴](#レビュー履歴)に前回までの経緯を残す。

## 前提（Round 2完了時点）

- 実案件・正本システムへの検索許可がまだ無いため、実データでのパイロットは未実施。引き続き開始しない。
- Round 1でCodexが `jira-task.schema.yaml`（`draft_id` / `trace_refs` / 構造化された `dependency_refs`）と `validation-run.schema.yaml` / [run-validation-dry-run.md](run-validation-dry-run.md) を追加した。
- Claude Codeがこれらの新形式を使ってダミーパイプラインを再実行し、[examples/pilot-feature/validation-run-002.md](../examples/pilot-feature/validation-run-002.md) として記録した。
- Round 2でCodexが `draft_id` の許容文字・一意性制約、`validation-run` の `actual_record_ref` 必須化、TBD-061への提案（YAML front matter方式、未実装）を追加した。ユーザーがこれらの結果を確認し、Round 2完了と判定した。
- [tbd-register.md](../docs/decisions/tbd-register.md) のTBD-058〜060は `実案件未検証` のまま維持。TBD-061は `検討中（提案あり・未実装）`。いずれも方式の確定・実装はまだ行わない。
- 既存のダミー成果物（`examples/pilot-feature/` 配下）は、Round 2の定義変更に対して適合済みであることを確認済み。業務上の理由での変更はしない。

## Codexへの実行プロンプト（次回更新待ち）

Round 3の具体的な依頼内容はまだPdM/POから指示されていない。以下はRound 2で使ったプロンプトを土台としたテンプレート。次回依頼する際は、背景・まず読んでほしいもの・依頼内容を最新の状況に合わせて更新してから使う。

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
- Round 2（2026-07-23、完了）: Round 1の修正を使ってダミーパイプラインを再実行した結果（validation-run-002.md）のレビューを依頼。Codexが `draft_id` の許容文字・一意性制約、`validation-run` の `actual_record_ref` 必須化を追加し、TBD-061にYAML front matter方式の提案（未実装）を追記。ユーザーが結果を確認し、TBD-058〜060は「実案件未検証」のまま維持で妥当と判定。既存のダミー成果物は変更不要と確認。
- Round 3（未実施）: 依頼内容は未定。着手条件・トリガーはPdM/POの指示待ち。候補としては、TBD-061（front matter方式）の具体化検討、または実案件パイロット開始の準備状況の再確認などが考えられるが、いずれも未確定であり推測で先取りしない。
