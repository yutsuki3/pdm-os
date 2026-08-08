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

   【決定】受領判断とQAの順序は「受領判断が先、QA依頼が後」で確定する。QA合格は受領判断の前提条件ではない。したがってQA依頼はPdM/POの受領判断（`accepted`）を経てから作成・送付する。

2. **QA依頼文書の草稿作成**
   [prompts/create-qa-request.md](../../prompts/create-qa-request.md) に従い、[templates/qa-request.md](../../templates/qa-request.md) を用いて、対象機能・関連する仕様書/Jiraタスク/実装（GitHub PR）へのリンク、テスト対象範囲を記載する。

3. **テスト範囲・環境の明記**
   検証環境（ステージング等）・対象ブラウザ/デバイス・除外項目を明記する。具体的な環境情報・命名はTBD。

4. **合否基準の明記**
   QA合格・不合格の判定基準（entry/exit criteria）を明記する。基準の詳細はTBD。

5. **送付**
   PdM/POが内容を確認し、SlackでQAチームへ送付する。【決定】送付証跡の正本はSlackの投稿とし、そのパーマリンクを `qa_requested` の完了条件とする（[source-of-truth.md](../architecture/source-of-truth.md)）。送付先チャンネル・投稿フォーマットはTBD。
   Work Itemを `qa_requested` に遷移。

6. **結果の反映**
   【決定】QA結果の正本はJira（QAチケットのステータスと結果記録）とする。そのチケットへの参照（[schemas/qa-result.schema.yaml](../../schemas/qa-result.schema.yaml) の `result_ref`）を確認した上で、`qa_passed` または `qa_failed` に遷移する。`qa_failed` 時の差し戻し先はTBD ([state-machine.md](../architecture/state-machine.md))。

## 入力/出力まとめ

| ステップ | 入力 | 出力 |
|---|---|---|
| QA依頼草稿 | 受領済み成果物 + 仕様書 + マージ済みPR | `templates/qa-request.md` を埋めた依頼文書 |
| 送付 | 承認済みQA依頼文書 | Slackの送付投稿（パーマリンクが送付証跡） |
| 結果反映 | JiraのQAチケット | `qa_passed` / `qa_failed` の判定と結果記録への参照 |

## 未確定事項

- 送付先Slackチャンネル・投稿フォーマット（スレッド運用の有無）
- SlackのQA依頼投稿とJiraのQAチケットの相互リンク方法
- entry/exit criteria の具体的な基準
- QA不合格時の差し戻し先・再依頼フロー
