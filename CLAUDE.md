# CLAUDE.md

このファイルは Claude Code 向けの追加ガイドです。共通ルールは [AGENTS.md](AGENTS.md) を先に読んでください。このファイルは AGENTS.md の内容を繰り返さず、Claude Code 固有の運用のみを記載します。

## リポジトリの現状

- 設計フェーズのみ。`src/` に実装コードは存在しません（`src/README.md` のみ）。
- テスト・ビルド・lintの類は現時点で存在しません。設計ドキュメントを追加・編集する作業が中心です。

## このフェーズでのClaude Codeの役割

現段階でClaude Codeが主に担当するのは以下。

- 業務フローの構造化 (`docs/workflows/`)
- 状態遷移の設計 (`docs/architecture/state-machine.md`)
- 成果物と責務の整理 (`docs/agents/`)
- 人間による承認点の設計 (`docs/architecture/approval-policy.md`)
- 不足している業務ルールの抽出（`TBD`として明記、[docs/decisions/tbd-register.md](docs/decisions/tbd-register.md) に集約）
- 文書とテンプレートの初期案作成 (`templates/`, `prompts/`, `examples/`)

後続でCodexが `schemas/` の具体化、ファイル構造、文書間の整合性レビューを担当する想定（[docs/agents/ai-tool-roles.md](docs/agents/ai-tool-roles.md) 参照）。そのため、このフェーズでは `schemas/*.yaml` を大きく作り込みすぎない。スキーマは草案レベルに留め、Codexのレビュー・具体化の余地を残す。

API・MCP連携、認証、データベース、クラウド構成の確定は、このフェーズのスコープ外（[AGENTS.md](AGENTS.md) 参照）。

## 作業の進め方

- 新しいドキュメントを追加する前に、[docs/index.md](docs/index.md) と該当ディレクトリの既存ファイルを確認し、重複や矛盾がないか確認する。
- 複数ファイルにまたがる大きな設計変更（例: 状態遷移の見直し、正本マッピングの変更）を行う場合は、着手前にユーザーに方針を確認する。単純なドキュメントの追記・誤字修正・TBDの解消は都度確認不要。
- ドキュメント作成において、存在しない組織名・ツールURL・担当者名を creatively に作らない。サンプルが必要な場合は `examples/pilot-feature/` のような明示的に架空と分かる命名を使う。

## TBDの扱い（Claude Code固有の運用）

- ユーザーから業務ルールに関する質問をされ、リポジトリ内に答えがない場合は、AskUserQuestion等で確認するか、確認できない場合は素直に `TBD` として記録する。ドキュメントの完成度を高めるために推測で埋めない。
- `TBD` を解消した場合は、該当ファイル内の `TBD` 表記と一緒に、なぜ確定したか（誰の発言・どの会話か）を簡潔に残す必要はない（会話ログが正本ではないため）。確定した内容のみを反映する。

## このリポジトリでのコミット運用

- ユーザーから明示的に依頼された場合のみコミットする（通常のグローバル運用と同じ）。
- コミットメッセージは日本語・英語どちらでも可。既存コミット (`first commit`) のスタイルに強くこだわる必要はない。
