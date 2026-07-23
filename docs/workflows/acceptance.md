# ワークフロー: 完了成果物の受領判断

## 目的

デザイン・実装が完了した成果物を仕様書と突き合わせ、PdM/POが受領するかどうかを判断するための材料を用意する。

## 関係者・エージェント

- Acceptance Agent: 仕様書と成果物の突き合わせ、チェックリスト作成
- PdM/PO: 最終的な受領判断

## 手順

1. **前提確認**
   Work Itemが `delivered` 状態であること（Jira上のタスクが完了報告されている）を確認する。

2. **成果物の特定**
   - 実装事実: GitHub上の対応するPR/コミット/タグを特定する。特定方法（Jiraチケット番号との紐付けルール）はTBD。
   - 受領原本: Google Drive上の対応するファイル（デザイン成果物、Google Docs等）を特定する。特定方法はTBD。

3. **突き合わせ**
   Acceptance Agentが [prompts/review-acceptance.md](../../prompts/review-acceptance.md) に従い、仕様書（Notion）の要件と、GitHub/Google Drive上の成果物を突き合わせ、[schemas/acceptance-report.schema.yaml](../../schemas/acceptance-report.schema.yaml) 形式のレポート草稿を作成する。GitHubとGoogle Driveで内容が重複・矛盾する場合は [deduplication-policy.md](../architecture/deduplication-policy.md) に従い、黙って解決せず記録する。
   Work Itemを `acceptance_review` に遷移。

4. **差異の提示**
   仕様と成果物に差異がある場合、Acceptance Agentは自動で合否を決めず、差異点を列挙するのみとする。

5. **受領判断**
   PdM/PO単独がレポートをもとに受領（`accepted`）または差し戻し（`rejected`）を判断する。仕様書の要件を満たしていることが基準。軽微な差異がある場合は差異を受領レポートに記録した上で受領し、別途フォローアップする。「軽微」と「重大（差し戻し対象）」の線引き基準、差し戻し時の記法はTBD ([approval-policy.md](../architecture/approval-policy.md))。

## 入力/出力まとめ

| ステップ | 入力 | 出力 |
|---|---|---|
| 突き合わせ | 仕様書 + GitHub実装 + Google Drive成果物 | `schemas/acceptance-report.schema.yaml` に基づくレポート草稿 |
| 受領判断 | レポート草稿 | 受領 (`accepted`) または差し戻し (`rejected`) |

## 未確定事項

- GitHub上の実装事実とJiraタスクの紐付けルール（コミットメッセージ規約、PRテンプレート等）
- Google Drive上の受領原本の特定方法（フォルダ構成・ステータスプロパティ）
- 「軽微な差異」と「重大な差異（差し戻し対象）」の線引き基準
- 差し戻し時の記録方法・再提出のフロー
