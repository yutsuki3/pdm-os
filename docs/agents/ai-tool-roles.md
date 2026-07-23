# Claude / Codex / Gemini / Notion AI の暫定的な役割

関連: [ADR-0005](../decisions/ADR-0005-model-agnostic-agent-roles.md) / [docs/vision/principles.md](../vision/principles.md) 原則7

## 前提

`docs/agents/*.md`（Orchestrator, Knowledge Agent, Specification Agent, Acceptance Agent, Release Agent）は **機能的な役割** の定義であり、特定のAIモデル・ツールを前提としない。本ドキュメントは、現時点でどのAIツールがどの機能をどの程度担うかの**暫定的な**割り当てを記録する。ツールの担当は将来変わりうるが、機能的な役割定義・業務フロー自体は変更されない設計とする（[docs/vision/principles.md](../vision/principles.md) 原則7）。

## 現時点の役割分担

| ツール | 位置づけ | 現時点で決定していること | 備考 |
|---|---|---|---|
| Claude Code | この設計フェーズの主担当 | 【事実】業務フローの構造化、状態遷移の設計、成果物と責務の整理、人間による承認点の設計、不足している業務ルールの抽出、文書とテンプレートの初期案作成を担当する（ユーザー指示） | `docs/` `templates/` `prompts/` `examples/` の初期案作成が中心 |
| Codex | 後続フェーズの担当 | 【事実】Schema・ファイル構造・文書間の整合性をレビューし、具体化する（ユーザー指示） | `schemas/*.yaml` の具体化が中心。Claude Codeが作った草案を精査する想定 |
| Gemini | 未定 | 【TBD】具体的な担当範囲は未指定 | 【提案・未確定】マルチモーダルな入力（画面キャプチャ・図表からのワイヤーフロー読み取り等）を要する作業の候補だが、確定していない |
| Notion AI | 未定 | 【TBD】具体的な担当範囲は未指定 | 【提案・未確定】正本であるNotion上で仕様書ページを直接下書き・要約する用途の候補だが、確定していない。Specification Agentの機能的役割とどう分担するかもTBD |

## 役割分担の原則

- 機能的な役割（`docs/agents/*.md`）とツール（本ドキュメント）は1対1に固定しない。1つの機能的役割を複数ツールが分担する、あるいは1つのツールが複数の機能的役割を担うことがありうる。
- ツール間の引き継ぎ（例: Claude Codeの草案をCodexがレビューする）では、[AGENTS.md](../../AGENTS.md) の事実・仮定・提案・決定のラベルを引き継ぎ、Codex側が「Claude Codeの提案」であることを認識できるようにする。
- 本ドキュメントの内容が確定情報のように扱われないよう、担当範囲が未定のツール（Gemini, Notion AI）については `TBD` / 【提案・未確定】であることを明記し続ける。

## 未確定事項

- Gemini・Notion AIの具体的な担当範囲・呼び出しタイミング。
- 複数ツールが同じ機能的役割を分担する場合の引き継ぎ方法・フォーマット。
- ツール間で意見が割れた場合（例: Codexのレビューがこのリポジトリの既存設計と矛盾する場合）の解決ルール。
