# PdM OS

PdM/PO (プロダクトマネージャー / プロダクトオーナー) の業務を支援・自動化するための設計リポジトリです。

**現時点はコードを実装していません。** README / AGENTS.md / CLAUDE.md / docs / schemas / templates / prompts / examples による設計フェーズです。実装 (src/) は将来フェーズで着手します。

## 目的

要求・要望の整理からリリースノート作成までの一連のPdM/PO業務を、人間の意思決定を維持したまま支援・自動化します。対象業務は以下の8つです。

1. 要求・要望から要件を整理する
2. 現行資料と過去資料を検索する
3. 仕様書を作成する
4. ワイヤーフローを作成する
5. Jiraのデザイン・実装タスクへ分解する
6. 完了成果物を受領判断する
7. QA依頼を作成する
8. リリースノートを作成する

## 情報の正本 (Source of Truth)

| ドメイン | 正本システム |
|---|---|
| 現行仕様と意思決定 | Notion |
| 過去仕様 | Confluence |
| 受領原本とGoogle Docs | Google Drive |
| タスク状態 | Jira |
| 実装事実 | GitHub |
| PdM OS自体の設計・ルール・状態管理 | このリポジトリ |

詳細は [docs/architecture/source-of-truth.md](docs/architecture/source-of-truth.md) を参照してください。

複数のシステムから同じ情報が得られる場合、検索経路が複数あること自体は問題ありませんが、同じ出所の情報を複数の独立した根拠として扱いません。情報の種類ごとに正本を優先し、矛盾は黙って解決せず記録します。詳細は [docs/architecture/deduplication-policy.md](docs/architecture/deduplication-policy.md)。

## リポジトリ構成

```
pdm-os/
├── README.md               本ファイル
├── AGENTS.md                AIエージェント向けの共通運用ルール
├── CLAUDE.md                 Claude Code向けの追加ガイド
│
├── docs/
│   ├── index.md              ドキュメント全体の目次
│   ├── vision/                目的・原則
│   ├── architecture/           アーキテクチャ・状態管理・承認ポリシー・重複排除方針
│   ├── workflows/              業務フローの詳細手順
│   ├── agents/                 各エージェントの役割定義・AIツール暫定役割分担
│   └── decisions/              ADR (Architecture Decision Record) ・未決定事項一覧
│
├── schemas/                  データ構造の定義 (YAML)
├── templates/                成果物のテンプレート (Markdown)
├── prompts/                  エージェント向けプロンプト定義
├── examples/                 サンプルケース (pilot-feature)
└── src/                      実装コード置き場 (現時点は未着手)
```

## 読む順番の目安

1. [docs/vision/pdm-os-vision.md](docs/vision/pdm-os-vision.md) — 何のためのシステムか、対象範囲
2. [docs/vision/principles.md](docs/vision/principles.md) — 設計原則
3. [docs/architecture/overview.md](docs/architecture/overview.md) — 全体構成
4. [docs/architecture/source-of-truth.md](docs/architecture/source-of-truth.md) / [docs/architecture/deduplication-policy.md](docs/architecture/deduplication-policy.md) / [docs/architecture/artifact-contracts.md](docs/architecture/artifact-contracts.md) — 正本・重複排除・成果物契約
5. [docs/architecture/state-machine.md](docs/architecture/state-machine.md) / [docs/architecture/approval-policy.md](docs/architecture/approval-policy.md) — 状態遷移と承認ポイント
6. [docs/workflows/](docs/workflows/) — 業務フロー別の詳細（要件からリリースまで）
7. [docs/agents/](docs/agents/) — エージェントの役割、[ai-tool-roles.md](docs/agents/ai-tool-roles.md) — Claude/Codex/Gemini/Notion AIの暫定役割分担
8. [schemas/](schemas/) / [templates/](templates/) / [prompts/](prompts/) — 実体となるデータ定義

## この段階の担当

現在は設計フェーズであり、Claude Codeが主に業務フローの構造化・状態遷移設計・成果物と責務の整理・承認ポイントの設計・不足している業務ルールの抽出・文書とテンプレートの初期案作成を担当しています。後続でCodexがSchema・ファイル構造・文書間の整合性をレビューし具体化します。詳細・他ツールとの暫定的な役割分担は [docs/agents/ai-tool-roles.md](docs/agents/ai-tool-roles.md) を参照してください。

## 未確定事項 (TBD) の扱い

このリポジトリでは、業務ルールが不明な場合に推測で埋めることを禁止しています。該当箇所は `TBD` と明記し、決定した時点でドキュメントを更新します。TBD の記法方針は [AGENTS.md](AGENTS.md) を、リポジトリ横断の一覧は [docs/decisions/tbd-register.md](docs/decisions/tbd-register.md) を参照してください。
