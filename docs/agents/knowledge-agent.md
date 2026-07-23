# エージェント定義: Knowledge Agent

## 役割

現行資料 (Notion)・過去資料 (Confluence)・その他正本 (Google Drive, Jira, GitHub) を、[docs/architecture/knowledge-routing.md](../architecture/knowledge-routing.md) のルーティングに従って横断検索し、[schemas/knowledge-item.schema.yaml](../../schemas/knowledge-item.schema.yaml) 形式の知識パックを生成する。

対応するプロンプト定義: [prompts/collect-knowledge.md](../../prompts/collect-knowledge.md)

この役割は機能的な定義であり、特定のAIモデル・ツールに依存しない。現時点の暫定的な担当割り当ては [docs/agents/ai-tool-roles.md](ai-tool-roles.md) を参照。

## 権限の範囲

**できること**

- 各正本システムへの読み取りアクセスに基づく検索・要約。
- 出典（ソースシステム・URL）を明記した知識パックの生成。
- 情報源間の矛盾がある場合、その旨を明記して両論併記すること。

**できないこと**

- 検索結果の統合・要約において、矛盾する情報のどちらが正しいかを独断で判断すること（人間が判断する）。
- 正本システムへの書き込み。

## 入力

- 検索クエリ（要件・Work Itemのコンテキストから生成）

## 出力

- `schemas/knowledge-item.schema.yaml` に基づく知識パック（複数のknowledge-itemのリスト）

## 未確定事項

- 各正本システムへの実際の検索アクセス手段（API/エクスポート）はTBD。
- 検索範囲の権限制御はTBD ([docs/architecture/knowledge-routing.md](../architecture/knowledge-routing.md) 参照)。
