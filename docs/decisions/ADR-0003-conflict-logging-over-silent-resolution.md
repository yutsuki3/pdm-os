# ADR-0003: 情報の重複・矛盾は黙って解決せず記録する

## ステータス

Accepted

## コンテキスト

PdM OSは複数の情報源（Notion, Confluence, Google Drive, Jira, GitHub）を横断的に検索する。同じ情報が複数の経路で見つかることや、情報源同士が矛盾することが起こりうる。

ユーザーから次の指示があった。「複数のサービスから同じ情報を取得できる場合があります。検索経路の重複は許可しますが、同じ情報を複数の独立した根拠として扱わないでください。情報の種類ごとに正本を優先し、矛盾は黙って解決せず記録してください。」

## 決定

1. **検索経路の重複は許可する。** Knowledge Agent等が複数システムを検索し、同じ論点について複数のヒットを得ること自体は問題としない。
2. **同一出所の情報を複数の独立した根拠として扱わない。** 出所（オリジン）が同じ情報は1つの根拠として数える。件数の多さを確からしさの根拠にしない。
3. **情報の種類（ドメイン）ごとに正本を優先する。** [source-of-truth.md](../architecture/source-of-truth.md) のマッピングに従う。
4. **矛盾は黙って解決しない。** 正本と非正本、あるいは想定外だが正本同士で内容が食い違う場合、どちらかを自動的に採用して片方を無視することはせず、矛盾がある事実自体を記録し、人間に提示する。

具体的な運用方法は [docs/architecture/deduplication-policy.md](../architecture/deduplication-policy.md) に記載する。

## 影響

- [schemas/knowledge-item.schema.yaml](../../schemas/knowledge-item.schema.yaml) の `conflict_notes` フィールドは、この決定に基づき「矛盾を記録する場所」として位置づけられる。出所の同一性をどう機械的に判定し、スキーマ上どう表現するかはCodexフェーズでの具体化対象。
- [prompts/collect-knowledge.md](../../prompts/collect-knowledge.md) / [prompts/review-acceptance.md](../../prompts/review-acceptance.md) に、この方針への準拠を明記した。

## 未確定事項

- 矛盾の記録先・フォーマット・エスカレーション先（[docs/decisions/tbd-register.md](tbd-register.md) 参照）。
- 「同一出所」の機械的な判定方法。
