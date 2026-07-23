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
   リリース単位は機能単位の随時リリースとする（QA合格したWork Itemごとに、合格次第リリースする。定期バッチは設けない）。

3. **リリースノート草稿作成**
   [prompts/create-release-note.md](../../prompts/create-release-note.md) に従い、各Work Itemの仕様書・Jiraタスク・GitHub実装（マージ済みPR/タグ）を参照し、[templates/release-note.md](../../templates/release-note.md) 形式で草稿を作成する。
   Work Itemを `release_note_drafting` に遷移。

4. **レビュー・承認**
   会議体（PdM/PO + エンジニアリード + QAリード）が内容を確認する。承認基準は、QA合格に加え、リリースノート草稿の内容確認、リスク（影響範囲・ロールバック手順等）の確認（[approval-policy.md](../architecture/approval-policy.md)）。

5. **公開**
   承認されたリリースノートを公開する。社内向けと顧客向けを別々に作成し、それぞれの公開先へ公開する（具体的なチャネル・フォーマットはTBD）。過去のリリースノートはNotion（現行仕様と同じ場所）にアーカイブする。
   Work Itemを `released` に遷移。

## 入力/出力まとめ

| ステップ | 入力 | 出力 |
|---|---|---|
| 草稿作成 | QA合格済みWork Item群 + 仕様書 + GitHub実装 | `templates/release-note.md` を埋めた草稿 |
| 公開 | 承認済み草稿 | 公開されたリリースノート（公開先TBD） |

## 未確定事項

- リリースノートの具体的な公開チャネル・フォーマット（社内向け/顧客向けそれぞれ）
