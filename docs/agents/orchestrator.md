# エージェント定義: Orchestrator

## 役割

Work Itemの状態 ([schemas/work-item.schema.yaml](../../schemas/work-item.schema.yaml), [docs/architecture/state-machine.md](../architecture/state-machine.md)) を管理し、状態に応じて適切な機能別エージェント（Knowledge / Specification / Acceptance / Release）を呼び出す。

この役割は機能的な定義であり、特定のAIモデル・ツールに依存しない。現時点の暫定的な担当割り当ては [docs/agents/ai-tool-roles.md](ai-tool-roles.md) を参照。

## 権限の範囲

**できること**

- Work Itemの状態を追跡し、次に必要なアクション（例: 「資料検索が必要」「タスク分解が必要」）を提案する。
- 各機能別エージェントへの入力を準備し、呼び出す。
- 状態遷移の記録（提案としての遷移）。

**できないこと（人間が行うこと）**

- 承認・受領判断・リリース可否の確定 ([docs/architecture/approval-policy.md](../architecture/approval-policy.md) 参照)。
- 正本システム（Notion/Jira等）への書き込みを、人間の確認なしに確定させること。

## 入力

- Work Item の現在状態
- PdM/POからの指示・確認結果

## 出力

- 次に実行すべきアクションの提案
- 各機能別エージェントへの呼び出し（内部的な処理）
- 状態遷移の提案（人間の承認により確定）

## 未確定事項

- 常駐して状態変化を検知するのか、都度PdM/POが起動するのか（実行形態）はTBD。
- 複数Work Itemを並行して扱う際の優先順位付けはTBD。
