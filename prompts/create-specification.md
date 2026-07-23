# プロンプト定義: create-specification

対象エージェント: [Specification Agent](../docs/agents/specification-agent.md)

## 目的

要件と知識パックから、[templates/specification.md](../templates/specification.md) 形式の仕様書草稿を作成する。

## 入力

- 要件 ([templates/requirement.md](../templates/requirement.md) の内容)
- 知識パック ([schemas/knowledge-item.schema.yaml](../schemas/knowledge-item.schema.yaml) のリスト、[prompts/collect-knowledge.md](collect-knowledge.md) の出力)

## 手順

1. 要件の背景・目的・制約を `background` / `goals` / `non_goals` に反映する。
2. 知識パック内の現行仕様 (`is_current_spec: true`) の情報を優先して整合性を確認する。過去仕様は経緯説明にのみ使う。
3. 機能要件・非機能要件を箇条書きで整理する。要件に明記されていない業務ルール（優先度基準・承認フロー等）は推測せず `open_questions` にTBDとして記載する。
4. 参照した知識アイテムをすべて `referenced_knowledge_items` / 「参照した資料」セクションに記載する。
5. ワイヤーフローが必要な場合は [templates/wireflow.md](../templates/wireflow.md) の作成を促す（本プロンプトの範囲外）。
6. `status` は常に `draft` から開始する。承認・Notion反映は行わない。

## 出力形式

`schemas/specification.schema.yaml` に準拠したMarkdown文書（`templates/specification.md` を埋めたもの）。例: [examples/pilot-feature/specification.md](../examples/pilot-feature/specification.md)

## 禁止事項

- 要件・知識パックに存在しない業務ルールを創作すること。
- `status` を `approved` に自ら変更すること（承認は人間が行う。[docs/architecture/approval-policy.md](../docs/architecture/approval-policy.md)）。
- 存在しないNotionページURLを `source_url` に記載すること。

## 未確定事項

- 非機能要件として必須の項目範囲はTBD。
- Notionへの反映方法・タイミングはTBD。
