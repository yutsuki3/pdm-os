<!--
これは架空のサンプルです。実在の組織・製品・PRとは関係ありません。
templates/qa-request.md を実際に埋めた例。schemas/qa-request.schema.yaml 準拠。
【テスト用】本ドキュメントは「フルパイプライン・ダミー検証」の一部。
acceptance-report.md の decision は実際には pending のままだが、
本検証では「テスト用に仮でaccepted扱いとする」ことを明示した上で後続工程を検証する。
実際の受領判断・QA依頼の送付ではない。
-->

# QA依頼: 通知設定のカスタマイズ機能（サンプル・テスト用仮受領）

- 対応Work Item: WI-SAMPLE-001
- 対応仕様書: SPEC-SAMPLE-001
- 依頼日: 2026-07-23
- 依頼者 (PdM/PO): サンプル太郎（架空）

【テスト用注記】対応する [acceptance-report.md](acceptance-report.md) の `decision` は実際には `pending`（FR-002, FR-003に `unclear` / `partially_met` の判定あり）。本検証では、パイプライン後続工程（QA依頼〜リリースノート）の成果物契約を確認する目的に限り、テスト用に「仮でaccepted」として扱う。実際の受領判断ではない。

## 対象機能の概要

通知種別ごとのON/OFF切り替え機能（FR-001〜FR-003）。[specification.md](specification.md) 参照。

## 関連リンク

- 仕様書 (Notion): TBD（本サンプルでは未反映）
- Jiraタスク: JT-SAMPLE-001〜004（草稿段階。実際のJira課題キーは未登録のためTBD）
- 実装 (GitHub PR): `example-org/example-repo#123`（架空、acceptance-report.md と同一参照）
- 受領レポート: [acceptance-report.md](acceptance-report.md)（前述のとおり実際は `pending`）

## テスト対象範囲

- 対象: 通知設定画面（wireflow.md S2）、FR-001〜FR-003
- 対象外: プッシュ通知・SMS通知（specification.md の Non-goals と同一）

## 検証環境

TBD — ステージング環境等の情報は未確定

## 合否基準 (Entry / Exit Criteria)

- Entry: TBD
- Exit: TBD

## リスク・注意点

- FR-002「即時反映」の定義がTBDのため、QA側でも判定基準が曖昧になる可能性がある（acceptance-report.md の discrepancies 参照）
- FR-003は既存ユーザー移行時の挙動が未確認（acceptance-report.md の discrepancies 参照）

## 送付先

TBD — QAチームへの送付方法（専用Jiraチケット/フォーム等）は未確定。本ドキュメントは送付前の草稿であり、送付は行っていない。
