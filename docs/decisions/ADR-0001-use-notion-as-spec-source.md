# ADR-0001: 現行仕様と意思決定の正本としてNotionを採用する

## ステータス

Accepted

## コンテキスト

PdM/POの業務では、現行仕様がどこにあるかが不明確になりがちで、Confluence上の古い情報と混同されるリスクがあった。ユーザーからの初期要求において、正本の割り当てが以下のように明示された。

- 現行仕様と意思決定: Notion
- 過去仕様: Confluence
- 受領原本とGoogle Docs: Google Drive
- タスク状態: Jira
- 実装事実: GitHub

## 決定

現行仕様と意思決定の正本をNotionとする。Specification Agentが作成する仕様書草稿は、最終的にNotion上のページへ反映されることを前提に設計する。Confluenceは過去仕様の参照専用とし、現行仕様の代替としては扱わない。

## 影響

- Knowledge Agentの検索ルーティング ([docs/architecture/knowledge-routing.md](../architecture/knowledge-routing.md)) は、現行仕様に関するクエリをNotion優先とする。
- 仕様書スキーマ ([schemas/specification.schema.yaml](../../schemas/specification.schema.yaml)) には、Notion上の正本ページを指す `source_url` を必須とする。
- Notion上の具体的なページ構成・反映プロセス・APIアクセス手段は本ADRの時点では未確定であり、TBDとして別途 [docs/architecture/source-of-truth.md](../architecture/source-of-truth.md) に記録する。

## 却下した代替案

- Confluenceを現行仕様の正本とする案: ユーザーの初期要求で過去仕様の置き場として明示されていたため却下。
- リポジトリ内（Markdown）を正本とする案: 「正本は外部システムにある」という設計原則 ([docs/vision/principles.md](../vision/principles.md)) に反するため却下。
