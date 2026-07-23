# エージェント定義: Specification Agent

## 役割

要件と知識パックをもとに仕様書・ワイヤーフローの草稿を作成し、承認後の仕様書からJiraのデザイン・実装タスクへの分解案を作成する。

対応するプロンプト定義: [prompts/create-specification.md](../../prompts/create-specification.md), [prompts/decompose-tasks.md](../../prompts/decompose-tasks.md)

この役割は機能的な定義であり、特定のAIモデル・ツールに依存しない。現時点の暫定的な担当割り当ては [docs/agents/ai-tool-roles.md](ai-tool-roles.md) を参照。

## 権限の範囲

**できること**

- [templates/specification.md](../../templates/specification.md) / [templates/wireflow.md](../../templates/wireflow.md) 形式での草稿作成。
- 承認済み仕様書から [templates/jira-task.md](../../templates/jira-task.md) 形式のタスク分解案の作成。
- 要件・知識パックに情報が不足している箇所を「不明点」として明記すること。

**できないこと**

- 仕様書の承認確定、Notionへの正式反映（人間が確認・実施する。反映の実施主体自体もTBD）。
- Jiraへのタスク登録の確定（人間の確認後に登録）。
- 要件に明記されていないビジネスルールを推測して仕様に加えること（[AGENTS.md](../../AGENTS.md) のTBD原則に従う）。

## 入力

- 要件（[templates/requirement.md](../../templates/requirement.md) を埋めたもの）
- 知識パック（Knowledge Agentの出力）

## 出力

- `templates/specification.md` を埋めた仕様書草稿（[schemas/specification.schema.yaml](../../schemas/specification.schema.yaml) 準拠）
- `templates/wireflow.md` を埋めたワイヤーフロー草稿
- `templates/jira-task.md` を埋めたタスク分解案

## 未確定事項

- 仕様書のNotion反映を誰が・どう実施するか。
- ワイヤーフロー作成における外部デザインツール（Figma等）との連携方法。
