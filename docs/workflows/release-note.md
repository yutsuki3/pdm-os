# ワークフロー: リリースノート作成

## 目的

QAに合格した機能・修正内容をまとめ、リリースノートを作成する。

## 関係者・エージェント

- Release Agent: リリースノート草稿作成
- PdM/PO: 内容確認・公開判断

## 手順

1. **前提確認**
   対象Work Itemが `qa_passed` 状態であることを確認する。

2. **対象範囲の確定**
   同一リリースに含める複数のWork Itemを確定する。リリース単位（バージョン、日次、週次等）の定義はTBD。

3. **リリースノート草稿作成**
   [prompts/create-release-note.md](../../prompts/create-release-note.md) に従い、各Work Itemの仕様書・Jiraタスク・GitHub実装（マージ済みPR/タグ）を参照し、[templates/release-note.md](../../templates/release-note.md) 形式で草稿を作成する。
   Work Itemを `release_note_drafting` に遷移。

4. **レビュー・承認**
   会議体（PdM/PO + エンジニアリード + QAリード）が内容を確認する。承認基準は、QA合格に加え、リリースノート草稿の内容確認、リスク（影響範囲・ロールバック手順等）の確認（[approval-policy.md](../architecture/approval-policy.md)）。

5. **公開**
   承認されたリリースノートを公開する。公開先（Notion、Confluence、社内向けSlack、顧客向けチャネル等）はTBD。
   Work Itemを `released` に遷移。

## 入力/出力まとめ

| ステップ | 入力 | 出力 |
|---|---|---|
| 草稿作成 | QA合格済みWork Item群 + 仕様書 + GitHub実装 | `templates/release-note.md` を埋めた草稿 |
| 公開 | 承認済み草稿 | 公開されたリリースノート（公開先TBD） |

## 未確定事項

- リリース単位の定義（バージョニング規則）
- リリースノートの公開先・フォーマット（社内向け/顧客向けを分けるか）
- 過去のリリースノートのアーカイブ先（Confluence想定だが未確認）
