# プロンプト定義: run-pilot-core-flow

対象エージェント: Claude Code（現段階の草稿作成・業務フロー構造化担当）。機能的には [Knowledge Agent](../docs/agents/knowledge-agent.md) と [Specification Agent](../docs/agents/specification-agent.md) を実行する。特定モデルへの依存を前提にしない。

## 目的

1件の実案件について、要求・要望から仕様書草稿、Jiraタスク草稿までを、外部正本への書き込みなしで作成・レビュー可能な状態にする。

## Claude Codeへの実行プロンプト

```text
PdM OSのコアフローパイロットを実施してください。

対象案件
- Work Item ID: <PdM/POが指定>
- 要求原文または原文への参照: <PdM/POが指定>
- 検索してよい正本の範囲: <Notion / Confluence / Google Drive / Jira / GitHub の範囲を明示>
- 現行仕様（Notion）への参照: <あれば指定、なければ「未確認」>
- 関連する過去資料への参照: <あれば指定、なければ「未確認」>

実施内容
1. prompts/collect-knowledge.md と docs/architecture/deduplication-policy.md に従い、知識パック草稿を作成する。
2. prompts/create-specification.md に従い、仕様書草稿を作成する。機能要件には FR-001 形式の要件IDを付ける。
3. ワイヤーフローが必要かを明示し、必要なら templates/wireflow.md の草稿を作る。必要性を判断できない場合はTBDにする。
4. 未確定の業務ルール、矛盾、出所不明の情報をTBDとして列挙する。事実・仮定・提案・決定を混同しない。
5. PdM/POから「仕様書は承認済み」と明示された場合だけ、prompts/decompose-tasks.md に従いJiraタスク草稿を作成する。明示されていない場合は、承認待ちとしてここで止める。

厳守事項
- Notion、Jira、Google Drive、GitHubを含む外部システムへ書き込まない。
- 承認、状態遷移、受領、QA合否、リリース可否を確定しない。
- 正本に存在しない情報、承認者、優先度、SLA、Jira設定、QA基準を推測しない。
- 同一出所の転記を独立した複数根拠として扱わない。矛盾は両論と出所を記録し、人間へ提示する。
- 実データ・機密情報・認証情報をこのリポジトリへ保存しない。必要な場合は正本への参照だけを出力する。

出力
- 要求・知識パック・仕様書・ワイヤーフロー・Jiraタスク草稿の一覧と外部正本への参照
- 各成果物の入力、出力、未解決TBD
- 人間のレビュー・承認が必要な箇所
- 実施結果を反映すべきPdM OS設計上の改善点
```

## 禁止事項

- PdM/POの明示なしに、実案件をこのリポジトリの `examples/` や `docs/` に保存すること。
- パイロットの結果を業務ルールの確定として扱うこと。
