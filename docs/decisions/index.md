# ADR一覧 (Architecture Decision Record)

| ID | タイトル | ステータス |
|---|---|---|
| [ADR-0001](ADR-0001-use-notion-as-spec-source.md) | 現行仕様と意思決定の正本としてNotionを採用する | Accepted |
| [ADR-0002](ADR-0002-repository-as-source-of-truth-for-pdm-os-design.md) | このリポジトリをPdM OS自体の設計・ルール・状態管理の正本とする | Accepted |
| [ADR-0003](ADR-0003-conflict-logging-over-silent-resolution.md) | 情報の重複・矛盾は黙って解決せず記録する | Accepted |
| [ADR-0004](ADR-0004-fact-assumption-proposal-decision-convention.md) | 事実・仮定・提案・決定を区別する文書規約を採用する | Accepted |
| [ADR-0005](ADR-0005-model-agnostic-agent-roles.md) | エージェント責務をモデル非依存に設計し、AIツールの役割は暫定とする | Accepted |

## 関連

- [tbd-register.md](tbd-register.md) — 未決定事項一覧（リポジトリ横断）

## ADRの追加方法

新しいADRを追加する場合、`docs/decisions/ADR-XXXX-<slug>.md` の形式でファイルを作成し、この表に追記する。ADRのテンプレート構成は ADR-0001 を参照。
