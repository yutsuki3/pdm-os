# ワークフロー: QA依頼作成

## 目的

受領判断を経た（または受領判断のために必要な）機能について、QAチームへ検証を依頼する文書を作成する。

## 関係者・エージェント

- Release Agent: QA依頼文書の草稿作成
- PdM/PO: 内容確認・送付判断
- QAチーム: 依頼の受け手（本リポジトリのスコープ外）

## 手順

1. **前提確認**
   Work Itemが `accepted` 状態であることを確認する。受領した機能は常に例外なくQAを通す（条件によるスキップは行わない）（[approval-policy.md](../architecture/approval-policy.md)）。

2. **QA依頼文書の草稿作成**
   [prompts/create-qa-request.md](../../prompts/create-qa-request.md) に従い、[templates/qa-request.md](../../templates/qa-request.md) を用いて、対象機能・関連する仕様書/Jiraタスク/実装（GitHub PR）へのリンク、テスト対象範囲を記載する。

3. **テスト範囲・環境の明記**
   検証環境（ステージング等）・対象ブラウザ/デバイス・除外項目を明記する。具体的な環境情報・命名はTBD。

4. **合否基準の明記**
   QA合格・不合格の判定基準（entry/exit criteria）を明記する。Entry基準は「受領済みでテスト環境にデプロイ済み」、Exit基準は「仕様書の受け入れ条件を全件テスト済みでバグなし」とする。

5. **送付**
   PdM/POが内容を確認し、チャットツール（例: Slack）でQAチームへ直接依頼する。送付に使ったメッセージへのリンクが、この依頼の送付証跡（正本）となる。
   Work Itemを `qa_requested` に遷移。

6. **結果の反映**
   QAチームが送付したチャットメッセージ（Slack等）を結果の正本とし、[schemas/qa-result.schema.yaml](../../schemas/qa-result.schema.yaml) 形式でメッセージへの参照を記録した上で、`qa_passed` または `qa_failed` に遷移する。`qa_failed` の場合はQA指摘を記載の上、Work Itemを `in_progress` に戻し、同じJiraタスクで再提出を待つ（[state-machine.md](../architecture/state-machine.md)）。再依頼条件の詳細はTBD。

## 入力/出力まとめ

| ステップ | 入力 | 出力 |
|---|---|---|
| QA依頼草稿 | 受領済み成果物 + 仕様書 + 実装 | `templates/qa-request.md` を埋めた依頼文書 |
| 送付 | 承認済みQA依頼文書 | QAチームへのチャットツール経由の依頼 |

## 未確定事項

- QA不合格時の再依頼条件の詳細
