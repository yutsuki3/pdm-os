# エージェント定義: Acceptance Agent

## 役割

GitHub上の実装事実、Google Drive上の受領原本と、仕様書（Notion）を突き合わせ、受領判断のためのレポート草稿を作成する。

対応するプロンプト定義: [prompts/review-acceptance.md](../../prompts/review-acceptance.md)

この役割は機能的な定義であり、特定のAIモデル・ツールに依存しない。現時点の暫定的な担当割り当ては [docs/agents/ai-tool-roles.md](ai-tool-roles.md) を参照。

## 権限の範囲

**できること**

- 仕様書の各要件と、GitHub実装・Google Drive成果物の対応関係を確認し、チェックリスト形式で提示する。
- 仕様と成果物の差異を検出し、明記する。

**できないこと**

- 受領（`accepted`）・差し戻し（`rejected`）の最終判断（[docs/architecture/approval-policy.md](../architecture/approval-policy.md) により人間が行う）。
- 差異の重大度を独断で「軽微だから合格」のように判定すること。

## 入力

- 仕様書（Notion、正本）
- 実装事実（GitHub上のPR/コミット/タグ）
- 受領原本（Google Drive上のファイル）

## 出力

- `schemas/acceptance-report.schema.yaml` に基づくレポート草稿（チェックリスト + 差異一覧）

## 未確定事項

- GitHub実装とJiraタスク/仕様書との紐付けルール。
- Google Drive上の受領原本の特定方法。
- 差異の重大度分類基準の有無。
