# プロンプト定義: create-release-note

対象エージェント: [Release Agent](../docs/agents/release-agent.md)

## 目的

QA合格済みのWork Item群から、[templates/release-note.md](../templates/release-note.md) 形式のリリースノート草稿を作成する。QA依頼の作成は [create-qa-request.md](create-qa-request.md) を使用する。

## 入力

- 対象Work Item群（`state: qa_passed`）
- 各Work Itemに紐づく仕様書・Jiraタスク・GitHub実装

## 手順 (リリースノート作成)

1. 対象リリースに含めるWork Itemを確定する。リリース単位の定義はTBD — 明示的に指定されない限り、渡されたWork Item群をそのまま1リリースとして扱う。
2. 各Work Itemについて、概要・仕様書リンク・Jiraタスクキー・GitHub実装（マージ済みPR/タグ）を1行にまとめる。
3. 既知の問題があれば `discrepancies` (受領レポート) やQA結果から拾い、「既知の問題」に記載する。なければ「なし」と明記する（省略しない）。
4. ロールアウト計画・公開先はTBDのまま出力する。

## 出力形式

[schemas/release-note.schema.yaml](../schemas/release-note.schema.yaml) に対応する、`templates/release-note.md` を埋めたMarkdown。

## 禁止事項

- 公開先・送付先を推測して具体的なURL/チャネル名を記載すること。
- 既知の問題セクションを、確認せずに「なし」と断定すること（不明な場合は「未確認」と記載する）。

## 未確定事項

- リリース単位の定義。
- リリースノート・QA依頼の公開先/送付先。
