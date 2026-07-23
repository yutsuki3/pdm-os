# プロンプト定義: request-codex-review

対象エージェント: Codex（Schema・ファイル構造・文書間の整合性のレビュー担当。[docs/agents/ai-tool-roles.md](../docs/agents/ai-tool-roles.md) 参照）

## 目的

Claude Codeが実施したパイロットのダミーデータ検証結果（[docs/workflows/pilot-core-flow.md](../docs/workflows/pilot-core-flow.md) の実施履歴、[examples/pilot-feature/dry-run-result.md](../examples/pilot-feature/dry-run-result.md)）をCodexにレビューさせ、Schema・テンプレート・文書間の整合性を確認・具体化する。

## 前提

- 実案件・正本システムへの検索許可がまだ無いため、実データでのパイロットは未実施。
- 架空サンプル (`examples/pilot-feature`) を用いた2段階のメカニクス確認ドライラン（第1部: 仕様書承認前で停止／第2部: テスト用仮承認でのフルパイプライン検証）の結果が [dry-run-result.md](../examples/pilot-feature/dry-run-result.md) に記録されている。
- この検証で新たに [tbd-register.md](../docs/decisions/tbd-register.md) のTBD-055〜060が判明している。

## Codexへの実行プロンプト

```text
PdM OS設計リポジトリ（pdm-os）で、Claude Codeが実施したパイロットのダミーデータ検証結果をレビューしてください。

## 背景
- このリポジトリは設計フェーズで、Claude Codeが業務フロー構造化・状態遷移設計・成果物整理・文書とテンプレートの初期案作成を担当し、Codexが後続でSchema・ファイル構造・文書間の整合性をレビュー・具体化する分担になっています（docs/agents/ai-tool-roles.md 参照）。
- 実案件・正本システムへの検索許可がまだ無いため、実データでのパイロットは実行できていません。代わりに、架空サンプル(examples/pilot-feature、通知設定のカスタマイズ機能)を使い、run-pilot-core-flow.md の手順とartifact-contracts.mdの成果物契約が機能するかを検証する「メカニクス確認ドライラン」を2段階で実施しました。

## まず読んでほしいもの
1. docs/workflows/pilot-core-flow.md の「実施履歴」セクション
2. examples/pilot-feature/dry-run-result.md（第1部・第2部の両方）
3. docs/decisions/tbd-register.md のTBD-055〜060（今回の検証で新たに判明した項目）

## レビュー対象の成果物一式
examples/pilot-feature/ 配下の全ファイル（input.md, knowledge-pack.yaml, specification.md, wireflow.md, jira-tasks/*.md, acceptance-report.md, qa-request.md, qa-result.yaml, release-note.md）。
これらは対応するschemas/*.yamlとtemplates/*.mdに沿って作成した想定です。

## 依頼内容
1. 各成果物が対応するschemas/*.yamlの必須項目・型を満たしているか確認する。
2. 成果物間の相互参照（work_item_id, specification_id, 要件ID(FR-001等), Jiraタスク草稿ID等）が実際に辿れるか確認する。
3. 特にTBD-058〜060（デザインタスクがワイヤーフロー画面IDを参照する場合の表現、Jira未登録の草稿同士の依存関係参照、受領pendingのまま後工程だけ仮定して検証する型）について、schemas/templates側で解消できる技術的な設計不備なのか、それとも業務ルール確定が必要なTBDなのかを切り分けてほしい。
4. 出力ファイル(examples/pilot-feature/以下)は、成果物契約(artifact-contracts.md)に照らして不足がなければ変更不要。修正が必要なのはschemas/templates/promptsなど、リポジトリ全体で再利用される定義側に限定する。
5. 業務ルール（承認者、優先度基準、Jira運用ルール等）を推測して確定しないこと。事実・仮定・提案・決定の区別(AGENTS.md参照)を維持し、決定を下す場合は必ずADRとして記録すること。

## 出力してほしいもの
- レビュー結果のサマリ（各schemaの適合状況、参照整合性、TBD-058〜060それぞれへの見解）
- 必要なschemas/templates/promptsの修正（あれば）
- tbd-register.mdの更新（新規TBDの追加、または既存TBDのステータス更新。解決したものがあれば理由を明記）
- 未解決のまま残すべき事項の一覧
```

## 禁止事項

- 業務ルール（承認者、優先度基準、Jiraプロジェクト構成等）を推測して確定すること。
- `examples/pilot-feature` の出力ファイルを、schemas/templatesの不備によらない理由で書き換えること（内容の良し悪しではなく契約適合性のレビューに限定する）。
- レビュー結果を人間の承認なしに「決定」として記録すること（ADR化する場合もステータスは提案段階から開始する）。
