# ADR-0002: このリポジトリをPdM OS自体の設計・ルール・状態管理の正本とする

## ステータス

Accepted

## コンテキスト

ADR-0001では、PdM/POが扱う業務データ（現行仕様、過去仕様、受領原本、タスク状態、実装事実）の正本を外部システムに割り当てた。一方で、PdM OSそのものの設計（業務フローの定義、Work Itemの状態遷移ルール、エージェントの責務分担、承認ポリシー等）をどこで管理するかは定義されていなかった。

ユーザーから、業務データの正本一覧に加えて「PdM OS自体の設計、ルール、状態管理: このリポジトリ」が明示された。

## 決定

PdM OS自体の設計・ルール・状態管理の**定義**の正本を、このリポジトリ（`pdm-os`）とする。具体的には以下を含む。

- 業務フローの定義 (`docs/workflows/`)
- Work Itemの状態遷移ルール (`docs/architecture/state-machine.md`)
- エージェントの責務分担 (`docs/agents/`)
- 承認ポリシー (`docs/architecture/approval-policy.md`)
- スキーマ・テンプレート・プロンプト定義 (`schemas/`, `templates/`, `prompts/`)

## 影響

- [source-of-truth.md](../architecture/source-of-truth.md) のマッピング表に6つ目のドメインとして追加した。
- 「このリポジトリ内の生成物は正本ではなく写しである」という従来の原則（[docs/vision/principles.md](../vision/principles.md) 原則1）は、業務データについては引き続き有効だが、PdM OS自体の設計についてはこのリポジトリが正本であるという例外を明示した。
- Work Itemの状態遷移**定義**の正本はこのリポジトリだが、個々のJiraチケットの進捗ステータスは引き続きJiraが正本である。両者を混同しないよう [state-machine.md](../architecture/state-machine.md) に注記した。
- 実際のWork Itemインスタンスをどこに永続化するか（DB等）は、本ADRの対象外であり `TBD`（API・DB設計を確定しない現フェーズのスコープ外）。

## 却下した代替案

- PdM OS自体の設計をNotion等の外部ツールで管理する案: 現段階では設計変更の追跡（Git履歴）とAIエージェントによる編集のしやすさを優先し、リポジトリ管理を採用した。将来的にNotion等への移行が必要になった場合は改めてADRを起こす。
