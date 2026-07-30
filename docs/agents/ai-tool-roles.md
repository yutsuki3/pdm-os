# Claude / Codex / Gemini / Notion AI の暫定的な役割

関連: [ADR-0005](../decisions/ADR-0005-model-agnostic-agent-roles.md) / [docs/vision/principles.md](../vision/principles.md) 原則7

## 前提

`docs/agents/*.md`（Orchestrator, Knowledge Agent, Specification Agent, Acceptance Agent, Release Agent）は **機能的な役割** の定義であり、特定のAIモデル・ツールを前提としない。本ドキュメントは、現時点でどのAIツールがどの機能をどの程度担うかの**暫定的な**割り当てを記録する。ツールの担当は将来変わりうるが、機能的な役割定義・業務フロー自体は変更されない設計とする（[docs/vision/principles.md](../vision/principles.md) 原則7）。

## 現時点の役割分担

| ツール | 位置づけ | 現時点で決定していること | 備考 |
|---|---|---|---|
| Claude Code | この設計フェーズの主担当 | 【事実】業務フローの構造化、状態遷移の設計、成果物と責務の整理、人間による承認点の設計、不足している業務ルールの抽出、文書とテンプレートの初期案作成を担当する（ユーザー指示） | `docs/` `templates/` `prompts/` `examples/` の初期案作成が中心 |
| Codex | 後続フェーズの担当 | 【事実】Schema・ファイル構造・文書間の整合性をレビューし、具体化する（ユーザー指示） | `schemas/*.yaml` の具体化が中心。Claude Codeが作った草案を精査する想定。レビュー依頼の実行プロンプトは [prompts/request-codex-review.md](../../prompts/request-codex-review.md) を参照 |
| Notion AI | Knowledge Agentの機能的役割を担当 | 【決定】資料収集（Notion/Confluence/Drive/Jira/GitHub横断）全体をNotion AIに委ねる | [knowledge-agent.md](knowledge-agent.md) の機能的役割をNotion AIが実行する。Claude Codeはこの資料収集を行わない |
| Gemini | 未使用 | 【決定】現時点では使用しない | 将来必要になった時点で改めて検討する |

## 役割分担の原則

- 機能的な役割（`docs/agents/*.md`）とツール（本ドキュメント）は1対1に固定しない。1つの機能的役割を複数ツールが分担する、あるいは1つのツールが複数の機能的役割を担うことがありうる。
- ツール間の引き継ぎ（例: Claude Codeの草案をCodexがレビューする）では、[AGENTS.md](../../AGENTS.md) の事実・仮定・提案・決定のラベルを引き継ぎ、Codex側が「Claude Codeの提案」であることを認識できるようにする。

## Notion AI → Claude Code の引き継ぎ（決定）

【決定】

- Notion AIは資料収集の結果を [knowledge-item.schema.yaml](../../schemas/knowledge-item.schema.yaml) 形式の知識パックとして出力する。Claude Code（Specification Agent以降）はこの知識パックを受け取って仕様書作成以降を担当する。ツールが変わってもスキーマ形式は共通のままとする。
- Notion AIとClaude Codeで資料の解釈・見解が割れた場合（例: 同じ資料の解釈が異なる）は、[ADR-0003](../decisions/ADR-0003-conflict-logging-over-silent-resolution.md) の矛盾記録方針に準じ、黙って解決せず記録した上でPdM/POが最終判断する。

## 未確定事項

- Notion AIの具体的な呼び出しタイミング・実行方法（Notion AI自体の操作方法はこのリポジトリのスコープ外）。
- Geminiを将来使う場合の担当範囲。
