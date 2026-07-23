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
   - 実装事実: GitHub上のリリースタグを単位とする。対象Work ItemにJiraタスクで紐付いた特定のリポジトリのみを参照する。コミット/PRにはJira課題キー（例: `PROJ-123`）を含める規約で紐付ける。
   - 受領原本: Google Drive上の対応するファイル（デザイン成果物、Google Docs等）を、ファイル名・ステータスプロパティで判別する（フォルダ構造は問わない）。

3. **突き合わせ**
   Acceptance Agentが [prompts/review-acceptance.md](../../prompts/review-acceptance.md) に従い、仕様書（Notion）の要件と、GitHub/Google Drive上の成果物を突き合わせ、[schemas/acceptance-report.schema.yaml](../../schemas/acceptance-report.schema.yaml) 形式のレポート草稿を作成する。GitHubとGoogle Driveで内容が重複・矛盾する場合は [deduplication-policy.md](../architecture/deduplication-policy.md) に従い、黙って解決せず記録する。
   Work Itemを `acceptance_review` に遷移。

4. **差異の提示**
   仕様と成果物に差異がある場合、Acceptance Agentは自動で合否を決めず、差異点を列挙するのみとする。

5. **受領判断**
   PdM/PO単独がレポートをもとに受領（`accepted`）または差し戻し（`rejected`）を判断する。仕様書の要件を満たしていることが基準。見た目・文言レベルの差異は軽微とし、受領レポートに記録した上で受領・フォローアップする。機能・動作に影響する差異は重大として差し戻す（[approval-policy.md](../architecture/approval-policy.md)）。
   差し戻し時は受領レポートに差し戻し理由を記載し、Work Itemを `in_progress` に戻して同じJiraタスクで再提出を待つ。

## 入力/出力まとめ

| ステップ | 入力 | 出力 |
|---|---|---|
| 突き合わせ | 仕様書 + GitHub実装 + Google Drive成果物 | `schemas/acceptance-report.schema.yaml` に基づくレポート草稿 |
| 受領判断 | レポート草稿 | 受領 (`accepted`) または差し戻し (`rejected`) |

## 未確定事項

- Google Driveのファイル名・ステータスプロパティの具体的な命名規則・値
