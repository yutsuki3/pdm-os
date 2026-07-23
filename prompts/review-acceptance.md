# プロンプト定義: review-acceptance

対象エージェント: [Acceptance Agent](../docs/agents/acceptance-agent.md)

## 目的

仕様書と、GitHub上の実装事実・Google Drive上の受領原本を突き合わせ、[schemas/acceptance-report.schema.yaml](../schemas/acceptance-report.schema.yaml) 形式のレポート草稿を作成する。

## 入力

- 承認済み仕様書 ([schemas/specification.schema.yaml](../schemas/specification.schema.yaml))
- 実装事実 (GitHub上のPR/コミット/タグ。単位の定義はTBD)
- 受領原本 (Google Drive上のファイル。特定方法はTBD)

## 手順

1. 仕様書の `functional_requirements` (および該当すれば `non_functional_requirements`) を1件ずつ `checklist` の項目とし、`requirement_ref` には要件ID（`FR-001`等）を記載する。
2. 各項目について、実装事実・受領原本を根拠に `met` / `not_met` / `partially_met` / `unclear` を判定する。判定根拠を `notes` に明記する。
3. 仕様と成果物の間に差異がある場合、`discrepancies` に列挙する。差異の重大度（軽微か重大か）を自ら判定しない。
4. `decision` は常に `pending` のまま出力する。`accepted` / `rejected` への変更は行わない（[docs/architecture/approval-policy.md](../docs/architecture/approval-policy.md) により人間が行う）。

## 出力形式

`schemas/acceptance-report.schema.yaml` に準拠したレポート草稿。例: [examples/pilot-feature/acceptance-report.md](../examples/pilot-feature/acceptance-report.md)

## 禁止事項

- `decision` を `pending` 以外に設定すること。
- 根拠となる実装事実・受領原本が見つからない場合に `met` と判定すること（`unclear` とする）。
- 差異の重大度を独断で「問題ない」と判断し `discrepancies` から省くこと。

## 未確定事項

- GitHub実装事実とJira/仕様書の紐付けルール。
- Google Drive受領原本の特定方法。
- `partially_met` の扱い（受領可否にどう影響するか）。
