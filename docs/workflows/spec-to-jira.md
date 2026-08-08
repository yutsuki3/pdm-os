# ワークフロー: 仕様書 → Jiraタスク分解

## 目的

承認済みの仕様書を、デザイン・実装それぞれのJiraタスクへ分解する。

## 関係者・エージェント

- Specification Agent: タスク分解の草稿作成
- Orchestrator: 前提状態を確認し、Specification Agentの呼び出しと状態遷移の提案を行う
- PdM/PO: タスク分解内容の確認・Jiraへの登録可否判断

## 手順

1. **前提確認**
   Work Itemが `spec_approved` 状態であることを確認する。

2. **タスク分解の草稿作成**
   [prompts/decompose-tasks.md](../../prompts/decompose-tasks.md) に従い、仕様書のセクション（機能要件・非機能要件・画面単位など）ごとに、デザインタスク・実装タスク候補を洗い出す。
   各タスクは [templates/jira-task.md](../../templates/jira-task.md) 形式で草稿化する。

   【決定】Jira上の階層は「1案件 (Work Item) = 1ストーリー、その配下に複数タスク」とする。課題タイプはJira標準（ストーリー / タスク）を使い、デザインと実装の区別は課題タイプではなく**ラベル**（`design` / `implementation`）で表す。

3. **タスク粒度・依存関係の確認**
   PdM/POがタスク分解案をレビューする。ストーリーは案件と1対1で対応するが、その配下のタスクをどこで切るか（1画面1タスクか、機能単位かなど）の粒度基準はTBD。

4. **Jiraへの登録**
   承認された分解案をJiraに登録する。まず案件のストーリーを作成し、その配下に各タスクを作成する。プロジェクトキーの具体値・必須カスタムフィールドはTBD ([source-of-truth.md](../architecture/source-of-truth.md))。
   登録後、ストーリーおよび各タスクを仕様書（Notion）・Work Itemと相互リンクする。

5. **状態遷移**
   Work Itemを `jira_tasks_created` に遷移し、以降の進捗はJira側のステータスを正とする。Work Item と1対1で対応するストーリーが、配下タスクの進捗を集約する単位となる（集約規則の詳細は [state-machine.md](../architecture/state-machine.md) 参照）。

## 入力/出力まとめ

| ステップ | 入力 | 出力 |
|---|---|---|
| タスク分解草稿 | 承認済み仕様書 | `templates/jira-task.md` を埋めたタスク案リスト |
| Jira登録 | 承認されたタスク案 | ストーリー1件 + 配下タスク (design/implementation ラベル付き) + 仕様書へのリンク |

## 未確定事項

- Jiraプロジェクトキーの具体値・必須カスタムフィールド
- ストーリー配下のタスクの分解粒度基準
- 見積り（ストーリーポイント等）を誰が・どの段階で入れるか
- デザインタスクと実装タスクの依存関係の表現方法（Jira上のリンク種別）
