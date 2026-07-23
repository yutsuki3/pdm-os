<!--
これは架空のサンプルです。実在の組織・製品・PR・ファイルとは関係ありません。
schemas/acceptance-report.schema.yaml に準拠した受領レポート草稿の例
(prompts/review-acceptance.md の出力イメージをMarkdownで表現)。
-->

# 受領レポート (草稿): 通知設定のカスタマイズ機能（サンプル）

- 対応Work Item: WI-SAMPLE-001
- 対応仕様書: SPEC-SAMPLE-001

## 参照した成果物

- 実装 (GitHub, サンプル): `example-org/example-repo#123` (架空のPR番号)
- 受領原本 (Google Drive, サンプル): `sample-drive-file-id-001` (架空のファイルID)

## チェックリスト

| 要件 | 判定 | 備考 |
|---|---|---|
| 1. 通知種別ごとにON/OFFを切り替えられる | met (サンプル) | 架空PR上で種別ごとのトグルUIが実装されている想定 |
| 2. 設定変更は即時反映される | unclear | 「即時反映」の厳密な定義が仕様書側でTBDのため判定不能 |
| 3. デフォルト設定は既存ユーザーの現行設定を引き継ぐ | partially_met (サンプル) | 新規ユーザーのデフォルトのみ確認でき、既存ユーザーの移行挙動は未確認という想定 |

## 差異一覧 (Discrepancies)

- 要件2の「即時反映」の定義が仕様書に存在しないため、実装が要件を満たすか判断できない。
- 要件3について、既存ユーザーの移行時の挙動を検証した記録が受領原本内に見当たらない（サンプルのため詳細は省略）。

## 判断

- decision: pending
- decided_by: TBD ([docs/architecture/approval-policy.md](../../docs/architecture/approval-policy.md) 参照)
- decided_at: —

このサンプルは、Acceptance Agentが `decision` を `pending` のまま出力し、最終判断をPdM/POに委ねる例を示すためのものです。
