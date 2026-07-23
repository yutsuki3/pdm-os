<!--
これは架空のサンプルです。実在の組織・製品とは関係ありません。
templates/specification.md を実際に埋めた例。
-->

# 仕様書: 通知設定のカスタマイズ機能（サンプル）

- 仕様書ID: SPEC-SAMPLE-001
- 対応Work Item: WI-SAMPLE-001
- ステータス: draft
- Notion正本URL (承認後に記載): TBD（このサンプルは草稿段階のため未反映）

## 背景

メール通知が多すぎるという問い合わせが増加している。現行は全通知一括ON/OFFのみで、種別ごとの制御ができない。2024年にも同様の検討があったが、当時は見送られている（Jira SAMPLE-88、理由詳細はTBD）。

## 目的 (Goals)

- 通知種別ごとにON/OFFを切り替えられるようにする
- メール通知に関する問い合わせを削減する

## 対象外 (Non-goals)

- プッシュ通知・SMS通知の個別設定（本要望の対象外、input.md 参照）

## 機能要件

- FR-001: ユーザーは通知設定画面で、通知種別ごとにON/OFFを切り替えられる
- FR-002: 設定変更は即時反映される（反映タイミングの厳密な定義はTBD）
- FR-003: デフォルト設定は既存ユーザーの現行設定（全ON相当）を引き継ぐ

## 非機能要件

TBD — このサンプルでは非機能要件の必須範囲が未確定であることを示すため空欄のままにしている。

## ワイヤーフロー

FR-001はユーザーが操作する画面（通知設定画面）を伴うため、ワイヤーフローが必要と判断した。[wireflow.md](wireflow.md) を参照。

## 参照した資料

| 出典 | タイトル | URL | 備考 |
|---|---|---|---|
| Notion (現行仕様) | 通知設定 仕様書 (現行) | https://notion.example.com/notification-settings-spec | 全ON/OFFのみの現行実装を確認 |
| Confluence (過去仕様) | 2024年 通知機能改善検討 | https://confluence.example.com/notification-improvement-2024 | 過去の見送り経緯 |
| Jira (過去チケット) | SAMPLE-88 | https://jira.example.com/browse/SAMPLE-88 | Won't Doでクローズ済み |

## 未解決の論点 (Open Questions)

- 2024年に見送られた理由の詳細（優先度判断の基準）: TBD
- 設定変更の反映タイミングの厳密な定義: TBD
- 優先度の判断基準: TBD
- 通知種別の一覧・粒度（[wireflow.md](wireflow.md) 作成時に判明した新規論点）: TBD

## 承認履歴

| 承認者 | 承認日 | 備考 |
|---|---|---|
| TBD | — | このサンプルは承認前の草稿 |
