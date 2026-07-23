# 情報取得と重複排除の方針

関連: [source-of-truth.md](source-of-truth.md) / [knowledge-routing.md](knowledge-routing.md) / [ADR-0003](../decisions/ADR-0003-conflict-logging-over-silent-resolution.md) / [schemas/knowledge-item.schema.yaml](../../schemas/knowledge-item.schema.yaml)

## 背景

PdM OSが扱う情報は、Notion / Confluence / Google Drive / Jira / GitHub の複数システムにまたがっており、同じ内容が複数のシステムに存在することがある（例: Jiraチケットの説明欄にNotion仕様書の内容が転記されている、Confluenceページに過去のSlack議事メモがコピーされている等）。

【事実】ユーザーからの指示: 「検索経路の重複は許可するが、同じ情報を複数の独立した根拠として扱わないこと」「情報の種類ごとに正本を優先し、矛盾は黙って解決せず記録すること」。本ドキュメントはこの指示を運用可能な方針に落とし込む。

## 原則1: 検索経路の重複は問題ではない

Knowledge Agentが1つの論点について複数のシステムを検索し、結果として同じ事実に複数の経路（例: NotionページとそれをJira課題が参照しているリンク）から辿り着くことは許容される。検索の網羅性を優先し、経路を絞る必要はない。

## 原則2: 「出所 (origin)」で情報を束ねる

複数の検索結果が同一の出所に由来する場合（転記・引用・リンクのみ等）、それらは **1つの根拠** として扱う。件数が多いことをもって確からしさが増したと判断しない。

- 各 [knowledge-item](../../schemas/knowledge-item.schema.yaml) は `source_system` と `source_id` を明記する。
- 同一内容が複数アイテムにまたがる場合、どちらが一次情報（オリジン）でどちらが転記・参照かを明記する。判定基準・スキーマ上の表現方法（例: `duplicate_of` 相当のフィールド）は Codex フェーズでのスキーマ具体化時に検討する。現時点では `conflict_notes` または本文中の注記で代替する。
- 出所が同じ情報を独立した複数の根拠として数え、「3箇所に書いてあるから確からしい」といった判断をしないこと。

## 原則3: ドメインごとの正本を優先する

[source-of-truth.md](source-of-truth.md) のマッピングに従い、情報の種類（ドメイン）ごとに1つの正本を優先する。

- 「今の仕様は何か」→ Notion優先。Confluence・Jira上に同旨の記載があっても、現行仕様の判断根拠としてはNotionを採用する。
- 「実装内容」→ GitHub優先。
- 正本以外のシステムの情報は、正本を補強する文脈情報として扱い、正本と対立する場合は次の原則4に従う。

## 原則4: 矛盾は黙って解決せず記録する

【決定】（[ADR-0003](../decisions/ADR-0003-conflict-logging-over-silent-resolution.md)）

- 正本と非正本の間、あるいは正本同士（本来ありえないはずだが、正本の切り替え漏れ等で発生しうる）で内容が矛盾する場合、自動的にどちらかを採用して片方を握りつぶさない。
- 矛盾を検知したら、両方の内容・出所・URLを提示し、「矛盾がある」という事実自体を明記する。
- 最終的にどちらを採用するかの判断は人間（PdM/PO）が行う。

## 適用箇所

- [Knowledge Agent](../agents/knowledge-agent.md) / [prompts/collect-knowledge.md](../../prompts/collect-knowledge.md): 知識パック生成時にこの方針を適用する。
- [Acceptance Agent](../agents/acceptance-agent.md) / [prompts/review-acceptance.md](../../prompts/review-acceptance.md): GitHub実装事実とGoogle Drive受領原本の間で内容が重複・矛盾する場合も同様に扱う。

## 矛盾記録の保存場所・エスカレーション（決定）

【決定】

- **記録先**: 矛盾はこのリポジトリ側で記録する（Work Itemに付随する矛盾ログ、[knowledge-item](../../schemas/knowledge-item.schema.yaml) の `conflict_notes` 等）。外部正本システムへの書き込みは行わない。
- **エスカレーション・SLA**: PdM/POが検知から1週間以内を目安に解決する。

## 未確定事項

- 「同一出所」をどう機械的に判定するか（テキスト類似度、リンクの有無、更新履歴の追跡など）はTBD（Codexフェーズでのスキーマ具体化対象）。
- 知識アイテムのスキーマに出所系統（オリジンのチェーン）をどう表現するかはTBD（Codexフェーズでのスキーマ具体化対象）。
- 矛盾記録の具体的なフォーマット・記録先のスキーマ表現、記録をクローズする権限者はTBD。
