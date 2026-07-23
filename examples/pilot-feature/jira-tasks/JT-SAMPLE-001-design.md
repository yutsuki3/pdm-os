<!--
これは架空のサンプルです。実在の組織・製品・Jira課題とは関係ありません。
templates/jira-task.md を実際に埋めた例。schemas/jira-task.schema.yaml 準拠。
【テスト用】このタスク草稿は「フルパイプライン・ダミー検証」の一部として、
仕様書が「テスト用に仮承認された」ものとして扱い作成した。実際の承認ではない。
【再検証】Codexレビューにより追加された draft_id / trace_refs / dependency_refs（構造化）形式に更新。
旧版で指摘した「ワイヤーフロー画面IDを参照できない」問題（TBD-058）は trace_refs で解消を確認。
-->

# Jiraタスク草稿: 通知設定画面のUIデザイン作成

- 草稿ID: JT-SAMPLE-001
- 対応仕様書: SPEC-SAMPLE-001
- 課題タイプ: Design（TBD — Jira上の正式な課題タイプ体系は未確定）
- プロジェクトキー: TBD

## 概要

[wireflow.md](../wireflow.md) の画面 S2（通知設定画面）のUIデザインを作成する。通知種別ごとのトグルリストのビジュアルデザインを含む。

## 受け入れ条件 (Acceptance Criteria)

- [ ] wireflow S2 に定義された要素（通知種別トグルのリスト）を満たすデザインが作成されている
  - 根拠: source_type: wireflow, source_ref: `wireflow.md`(SPEC-SAMPLE-001), item_ref: S2
- [ ] 通知種別の一覧・粒度（wireflow.md のオープンクエスチョン）についてデザイン上の暫定案が示されている
  - 根拠: source_type: wireflow, source_ref: `wireflow.md`(SPEC-SAMPLE-001), item_ref: S2（オープンクエスチョン欄）

## 関連リンク

- 仕様書 (Notion): TBD（承認後に反映されるURL。本サンプルでは未反映）
- ワイヤーフロー: [wireflow.md](../wireflow.md) 画面ID S2
- 親Work Item: WI-SAMPLE-001
- 依存する他タスク: なし（本タスクが後続タスクの前提）

## 見積り

TBD — 見積り単位・入力タイミングは未確定

## ラベル・コンポーネント

TBD

## 担当候補

TBD

---

【所見（更新）】旧版では、受け入れ条件がワイヤーフローの画面ID（S2）を参照する必要があるのに `requirement_ref` が仕様書の要件IDしか想定していない、という表現不足を指摘した（TBD-058）。Codexのレビューにより `trace_refs`（`source_type: specification / wireflow / jira_task_draft / jira_issue`）が導入され、上記のとおり `source_type: wireflow` で自然に表現できることを確認した。TBD-058のスキーマ・テンプレート上の不足は解消。ただし実案件での運用検証（実際のJira登録・実際のワイヤーフローツールとの整合等）は未実施。
