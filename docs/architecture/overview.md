# アーキテクチャ概要

## 全体構成

PdM OSは、1つのOrchestratorと4つの機能別エージェント、5つの外部正本システム、そしてPdM OS自体の設計・ルール・状態管理の正本である本リポジトリから構成される。

各エージェントは特定のAIモデル・ツールに紐づかない**機能的な役割**として定義する。現時点でのClaude/Codex/Gemini/Notion AIへの暫定的な担当割り当ては [docs/agents/ai-tool-roles.md](../agents/ai-tool-roles.md) を参照。担当ツールが変わっても、下記の役割定義と業務フロー自体は維持される想定。

```
                     ┌─────────────────────────┐
                     │        PdM / PO          │  ← 各ゲートで最終判断
                     └────────────┬─────────────┘
                                  │ 承認・指示
                                  ▼
                     ┌─────────────────────────┐
                     │      Orchestrator         │  (docs/agents/orchestrator.md)
                     │  Work Item の状態を管理      │
                     └───┬───────┬───────┬──────┘
                         │       │       │
          ┌──────────────┘       │       └──────────────┐
          ▼                      ▼                      ▼
┌───────────────────┐  ┌───────────────────┐  ┌───────────────────┐
│  Knowledge Agent    │  │ Specification Agent │  │  Acceptance Agent   │
│ (資料検索)            │  │ (仕様書/ワイヤーフロー) │  │ (受領判断支援)         │
└─────────┬──────────┘  └─────────┬──────────┘  └─────────┬──────────┘
          │                       │                       │
          ▼                       ▼                       ▼
   Notion / Confluence      Notion (書込先)         GitHub / Google Drive
   Google Drive / Jira                                     │
   GitHub (読取専用)                                         ▼
                                                    ┌───────────────────┐
                                                    │   Release Agent     │
                                                    │ (QA依頼/リリースノート)│
                                                    └─────────┬──────────┘
                                                              │
                                                              ▼
                                                       QA / リリース先 (TBD)
```

## 構成要素

| 要素 | 役割 | 定義ファイル |
|---|---|---|
| Orchestrator | Work Itemの状態遷移を管理し、各エージェントを呼び出す | [agents/orchestrator.md](../agents/orchestrator.md) |
| Knowledge Agent | Notion/Confluence/Drive/Jira/GitHubを横断検索し、知識パックを生成 | [agents/knowledge-agent.md](../agents/knowledge-agent.md) |
| Specification Agent | 要件と知識パックから仕様書・ワイヤーフロー草稿を作成 | [agents/specification-agent.md](../agents/specification-agent.md) |
| Acceptance Agent | GitHub/Google Driveの成果物と仕様書を突き合わせ、受領判断材料を作成 | [agents/acceptance-agent.md](../agents/acceptance-agent.md) |
| Release Agent | QA依頼・リリースノートの草稿を作成 | [agents/release-agent.md](../agents/release-agent.md) |

## ライフサイクルとの対応

各業務フローの詳細手順は [docs/workflows/](../workflows/) を、状態遷移の全体像は [state-machine.md](state-machine.md) を参照。

1. 要求・要望 → [workflows/requirement-to-spec.md](../workflows/requirement-to-spec.md)
2. 仕様書 → Jiraタスク → [workflows/spec-to-jira.md](../workflows/spec-to-jira.md)
3. 成果物受領 → [workflows/acceptance.md](../workflows/acceptance.md)
4. QA依頼 → [workflows/qa-request.md](../workflows/qa-request.md)
5. リリースノート → [workflows/release-note.md](../workflows/release-note.md)

## データの流れの原則

- 各エージェントは正本システムに対して基本は**読み取り**を行う。書き込みを行うのは、仕様書のNotionへの反映など、明示的に許可された箇所のみ（[source-of-truth.md](source-of-truth.md) 参照）。
- リポジトリ内の `examples/` `templates/` に生成される草稿は中間成果物であり、正本ではない。

## 未確定事項

- Orchestratorの実行形態（常駐サービスか、都度起動のCLIか、Claude Code上のスキルか）は TBD。
- 各エージェントの実装技術（LLMモデル・フレームワーク）は TBD。このリポジトリは設計フェーズのため未決定。API・MCP連携・認証・DB・クラウド構成の確定はこのフェーズのスコープ外（[AGENTS.md](../../AGENTS.md) 参照）。

まとめて確認する場合は [docs/decisions/tbd-register.md](../decisions/tbd-register.md) を参照。
