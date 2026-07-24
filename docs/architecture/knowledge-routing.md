# 知識ルーティング

Knowledge Agent ([docs/agents/knowledge-agent.md](../agents/knowledge-agent.md)) が、検索クエリの種類に応じてどの正本システムを、どの優先順位で検索するかを定義する。

## ルーティングの基本方針

1. 「今の仕様・意思決定は何か」を問うクエリ → Notion を最優先。
2. 「なぜこの仕様になったか」「過去はどうだったか」を問うクエリ → Confluence を優先し、Notionの意思決定ログを補助的に参照。
3. 「成果物の原本はどこにあるか」を問うクエリ → Google Drive。
4. 「このタスクは今どういう状態か」を問うクエリ → Jira。
5. 「実際にどう実装されたか」を問うクエリ → GitHub。

## ルーティング表

| クエリの種類 | 第一検索先 | 補助検索先 | 備考 |
|---|---|---|---|
| 現行仕様の確認 | Notion | — | Confluenceは参照しない（過去仕様との混同を避ける） |
| 過去の経緯・意思決定の背景 | Confluence | Notion（意思決定ログ） | |
| 類似要望・過去の要件 | Confluence, Notion | Jira（過去チケット） | |
| 受領対象の原本所在 | Google Drive | Notion（該当仕様書からのリンク） | |
| タスクの進捗状況 | Jira | — | |
| 実装内容の確認 | GitHub | Jira（紐づくチケット） | |

## 複数システムにまたがる検索の扱い

- Knowledge Agentは複数システムから得た結果を「知識パック」(`schemas/knowledge-item.schema.yaml`) としてまとめ、各アイテムに出典システムを明記する。
- 複数システムを検索した結果、同じ経路・同じ論点で複数のヒットが得られること自体は問題ない（検索経路の重複は許可）。ただし、同じ出所に由来する情報を複数の独立した根拠として扱わない。詳細な運用ルールは [deduplication-policy.md](deduplication-policy.md) を参照。
- 出典が異なる情報が矛盾する場合、Knowledge Agentは自動的に統合・要約せず、両方を提示し矛盾がある旨を明記する（判断は人間が行う。[ADR-0003](../decisions/ADR-0003-conflict-logging-over-silent-resolution.md)）。

## 権限制御（決定）

【決定】Knowledge Agentは、PdM/PO自身がアクセス権限を持つ範囲の情報を全て検索対象とする。PdM/POが閲覧権限を持たない情報（他部門限定ページ等）を除外する特別な制御は設けない。

## 未確定事項

- 各システムへの検索アクセス方法（API連携か、エクスポートデータの検索か）はTBD。
- 検索結果のランキング・関連度スコアの算出方法はTBD（`schemas/knowledge-item.schema.yaml` の `relevance_score` は現時点でプレースホルダ）。
