# プロンプト定義: collect-knowledge

対象エージェント: [Knowledge Agent](../docs/agents/knowledge-agent.md)

## 目的

要件・Work Itemのコンテキストから検索クエリを組み立て、Notion / Confluence / Google Drive / Jira / GitHub を横断検索し、知識パックを生成する。

## 入力

- Work Item ([schemas/work-item.schema.yaml](../schemas/work-item.schema.yaml))
- 要件テキスト ([templates/requirement.md](../templates/requirement.md) の内容)

## 手順

1. [docs/architecture/knowledge-routing.md](../docs/architecture/knowledge-routing.md) のルーティング表に従い、クエリの種類（現行仕様確認/過去経緯/類似要望/受領原本所在/タスク状況/実装確認）を判定する。
2. 判定した種類に応じた優先順位で各正本システムを検索する。
3. 検索結果を [schemas/knowledge-item.schema.yaml](../schemas/knowledge-item.schema.yaml) 形式に変換する。各アイテムに `source_system` を必ず明記する。
4. Notion由来（現行仕様）とConfluence由来（過去仕様）は `is_current_spec` フラグで明確に区別する。混同しない。
5. [docs/architecture/deduplication-policy.md](../docs/architecture/deduplication-policy.md) に従い、同じ出所に由来する複数のヒットを1つの根拠として扱う。検索経路が複数あること自体は問題ないが、件数の多さを確からしさとして扱わない。
   転記・引用元を確認できた場合は各アイテムの `origin` に記録し、確認できない場合は `origin.origin_status: unknown` とする。出所を推測して補完しない。
6. 複数の出典が矛盾する情報を含む場合、統合・要約せず、両方を提示し `conflict_notes` に矛盾がある旨を記載する（[ADR-0003](../docs/decisions/ADR-0003-conflict-logging-over-silent-resolution.md)）。

## 出力形式

`schemas/knowledge-item.schema.yaml` に準拠したアイテムのリスト（知識パック）。例: [examples/pilot-feature/knowledge-pack.yaml](../examples/pilot-feature/knowledge-pack.yaml)

## 禁止事項

- 出典の異なる情報を、出典を明記せずに1つの結論に統合すること。
- 検索範囲・アクセス手段が不明な場合に、存在しない資料をあるかのように記述すること。
- `relevance_score` の算出方法が未確定であることを踏まえ、スコアの意味を過大に主張すること。

## 未確定事項

- 各正本システムへの実際の検索アクセス手段（API/エクスポート）はTBD。
- 検索範囲の権限制御はTBD。
