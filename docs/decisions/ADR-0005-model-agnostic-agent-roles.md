# ADR-0005: エージェント責務をモデル非依存に設計し、AIツールの役割は暫定とする

## ステータス

Accepted

## コンテキスト

PdM OSの設計・運用には、複数のAIツール（Claude Code, Codex, Gemini, Notion AI等）が関与しうる。ユーザーから「モデル固有の能力に依存しすぎない設計にしてください。将来Claude、Codex、Gemini、Notion AIなどの担当を変更しても、業務フロー自体は維持できる構造にしてください」という指示があった。また、この段階ではClaude Codeが業務フロー構造化等を担当し、後続でCodexがSchema・ファイル構造・整合性レビューを担当することが明示された。

## 決定

1. `docs/agents/*.md`（Orchestrator, Knowledge Agent, Specification Agent, Acceptance Agent, Release Agent）は、特定のAIモデル・ツールに依存しない **機能的な役割** として定義する。
2. 現時点でのAIツールごとの担当割り当ては、機能的な役割定義とは別のドキュメント [docs/agents/ai-tool-roles.md](../agents/ai-tool-roles.md) に切り離して記録し、「暫定」であることを明記する。
3. Claude Codeの現段階の担当（業務フロー構造化、状態遷移設計、成果物と責務の整理、承認点設計、不足ルール抽出、文書・テンプレート初期案作成）と、Codexの後続の担当（Schema・ファイル構造・文書間整合性のレビューと具体化）は事実として記録するが、Gemini・Notion AIの担当は未定 (`TBD`) のまま扱う。

## 影響

- [docs/vision/principles.md](../vision/principles.md) に原則7（モデル・ツールに依存しない設計）を追加した。
- `docs/agents/*.md` 各ファイルに、機能的役割であることと `ai-tool-roles.md` への参照を追記した。

## 未確定事項

- Gemini・Notion AIの具体的な担当範囲。
- 複数ツールが同じ機能的役割を分担する場合の引き継ぎ・整合性確保の方法。
