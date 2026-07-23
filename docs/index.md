# ドキュメント目次

## vision — 目的と原則

- [pdm-os-vision.md](vision/pdm-os-vision.md) — 何のためのシステムか、対象ユーザー、スコープ
- [principles.md](vision/principles.md) — 設計原則

## architecture — 全体構成

- [overview.md](architecture/overview.md) — システム全体の構成
- [source-of-truth.md](architecture/source-of-truth.md) — 正本マッピングと参照ルール（6ドメイン）
- [deduplication-policy.md](architecture/deduplication-policy.md) — 情報取得と重複排除の方針
- [knowledge-routing.md](architecture/knowledge-routing.md) — 検索・知識ルーティングのルール
- [artifact-contracts.md](architecture/artifact-contracts.md) — 成果物の入力・出力・Schema・正本の対応
- [state-machine.md](architecture/state-machine.md) — Work Item のライフサイクル（案件の状態遷移）
- [approval-policy.md](architecture/approval-policy.md) — 承認ゲートと承認者 (多くがTBD)

## workflows — 業務フロー詳細

- [requirement-to-spec.md](workflows/requirement-to-spec.md) — 要求・要望 → 要件整理 → 仕様書
- [spec-to-jira.md](workflows/spec-to-jira.md) — 仕様書 → Jiraタスク分解
- [acceptance.md](workflows/acceptance.md) — 成果物の受領判断
- [qa-request.md](workflows/qa-request.md) — QA依頼作成
- [release-note.md](workflows/release-note.md) — リリースノート作成

## agents — エージェント定義

- [orchestrator.md](agents/orchestrator.md) — 全体調整・状態管理
- [knowledge-agent.md](agents/knowledge-agent.md) — 現行/過去資料検索
- [specification-agent.md](agents/specification-agent.md) — 仕様書・ワイヤーフロー作成支援
- [acceptance-agent.md](agents/acceptance-agent.md) — 受領判断支援
- [release-agent.md](agents/release-agent.md) — QA依頼・リリースノート作成支援
- [ai-tool-roles.md](agents/ai-tool-roles.md) — Claude/Codex/Gemini/Notion AIの暫定的な役割分担

## decisions — ADR・未決定事項

- [index.md](decisions/index.md) — ADR一覧
- [ADR-0001-use-notion-as-spec-source.md](decisions/ADR-0001-use-notion-as-spec-source.md)
- [ADR-0002-repository-as-source-of-truth-for-pdm-os-design.md](decisions/ADR-0002-repository-as-source-of-truth-for-pdm-os-design.md)
- [ADR-0003-conflict-logging-over-silent-resolution.md](decisions/ADR-0003-conflict-logging-over-silent-resolution.md)
- [ADR-0004-fact-assumption-proposal-decision-convention.md](decisions/ADR-0004-fact-assumption-proposal-decision-convention.md)
- [ADR-0005-model-agnostic-agent-roles.md](decisions/ADR-0005-model-agnostic-agent-roles.md)
- [tbd-register.md](decisions/tbd-register.md) — 未決定事項一覧（リポジトリ横断）

## 関連

- [schemas/](../schemas/) — データ構造定義
- [templates/](../templates/) — 成果物テンプレート
- [prompts/](../prompts/) — エージェント向けプロンプト
- [examples/pilot-feature/](../examples/pilot-feature/) — サンプルケース
