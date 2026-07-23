# ワークフロー: QA依頼作成

## 目的

受領判断を経た（または受領判断のために必要な）機能について、QAチームへ検証を依頼する文書を作成する。

## 関係者・エージェント

- Release Agent: QA依頼文書の草稿作成
- PdM/PO: 内容確認・送付判断
- QAチーム: 依頼の受け手（本リポジトリのスコープ外）

## 手順

1. **前提確認**
   Work Itemが `accepted` 状態であることを確認する。受領前にQAを挟む運用があるかどうかはTBD（[approval-policy.md](../architecture/approval-policy.md)）。

2. **QA依頼文書の草稿作成**
   [templates/qa-request.md](../../templates/qa-request.md) を用いて、対象機能・関連する仕様書/Jiraタスク/実装（GitHub PR）へのリンク、テスト対象範囲を記載する。

3. **テスト範囲・環境の明記**
   検証環境（ステージング等）・対象ブラウザ/デバイス・除外項目を明記する。具体的な環境情報・命名はTBD。

4. **合否基準の明記**
   QA合格・不合格の判定基準（entry/exit criteria）を明記する。基準の詳細はTBD。

5. **送付**
   PdM/POが内容を確認し、QAチームへ送付する。送付先・送付方法（Jira上のQA用チケット、専用フォーム等）はTBD。
   Work Itemを `qa_requested` に遷移。

6. **結果の反映**
   QA結果に応じて `qa_passed` または `qa_failed` に遷移する。`qa_failed` 時の差し戻し先はTBD ([state-machine.md](../architecture/state-machine.md))。

## 入力/出力まとめ

| ステップ | 入力 | 出力 |
|---|---|---|
| QA依頼草稿 | 受領済み成果物 + 仕様書 + 実装 | `templates/qa-request.md` を埋めた依頼文書 |
| 送付 | 承認済みQA依頼文書 | QAチームへの依頼（送付先・方法TBD） |

## 未確定事項

- 受領判断とQA依頼の順序（QA合格が受領の前提条件かどうか）
- QA依頼の送付先・送付方法
- entry/exit criteria の具体的な基準
- QA不合格時の差し戻し先・再依頼フロー
