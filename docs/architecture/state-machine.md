# Work Item ライフサイクル (状態機械)

Work Item ([schemas/work-item.schema.yaml](../../schemas/work-item.schema.yaml)) は、1つの要求・要望が要件化され、仕様化・実装・受領・リリースされるまでの単位を表す。

【決定】この状態機械（状態一覧・遷移ルール）の**定義**の正本はこのリポジトリである（[source-of-truth.md](source-of-truth.md) 参照）。ただし、`in_progress` 配下の個々のJiraチケットの進捗ステータスは引き続きJiraが正本であり、本状態機械はそれらを集約したWork Item全体のライフサイクルを表す。実際のWork Itemインスタンスの状態をどこに永続化するか（DB等）は、この設計フェーズでは未確定（`TBD`、[AGENTS.md](../../AGENTS.md) の「この段階のスコープ」参照）。

## 状態一覧

| 状態 | 説明 | 主な担当 |
|---|---|---|
| `requested` | 要求・要望が寄せられ、まだ整理されていない | PdM/PO |
| `requirement_defined` | 要件として整理・合意された | PdM/PO (Orchestrator支援) |
| `spec_drafting` | 仕様書・ワイヤーフローを草稿中 | Specification Agent |
| `spec_review` | 仕様書がレビュー中 | PdM/PO, 関係者 |
| `spec_approved` | 仕様書が承認された（Notionへ反映） | PdM/PO (承認者はTBD) |
| `jira_tasks_created` | 仕様書からJiraのデザイン・実装タスクへ分解済み | Specification Agent, Orchestrator |
| `in_progress` | Jira上でタスクが進行中 | デザイナー/エンジニア (Jira側で管理) |
| `delivered` | 実装・デザイン成果物が提出された | エンジニア/デザイナー |
| `acceptance_review` | 受領判断を実施中 | Acceptance Agent, PdM/PO |
| `accepted` | 受領判断で合格 | PdM/PO |
| `rejected` | 受領判断で差し戻し | PdM/PO |
| `qa_requested` | QA依頼を作成・送付済み | Release Agent, PdM/PO |
| `qa_passed` / `qa_failed` | QA結果 | QAチーム |
| `release_note_drafting` | リリースノート草稿中 | Release Agent |
| `released` | リリース完了 | PdM/PO |

## 状態遷移図

```
requested
   │ 要件整理
   ▼
requirement_defined
   │ 仕様書草稿開始
   ▼
spec_drafting ──┐
   │            │ 資料検索・差し戻し
   ▼            │
spec_review ────┘
   │ 承認 (承認者TBD)
   ▼
spec_approved
   │ タスク分解
   ▼
jira_tasks_created
   │ Jira側で進行
   ▼
in_progress
   │ 成果物提出
   ▼
delivered
   │ 受領判断
   ▼
acceptance_review ──► rejected ──(差し戻し)──► in_progress
   │ 受領
   ▼
accepted
   │ QA依頼
   ▼
qa_requested ──► qa_failed ──(差し戻し)──► in_progress (もしくはTBD)
   │ QA合格
   ▼
qa_passed
   │ リリースノート作成
   ▼
release_note_drafting
   │ リリース
   ▼
released
```

## 未確定事項

- `spec_review` → `spec_approved` の承認者・承認条件は TBD ([approval-policy.md](approval-policy.md) 参照)。
- `rejected` / `qa_failed` からの差し戻し先が常に `in_progress` でよいか（`requirement_defined` に戻すケースがあるか）はTBD。
- 1つのWork Itemが複数のJiraタスクに分解された場合、それぞれの進捗をどうWork Item全体の状態に集約するかはTBD。
- 状態遷移をJiraのステータスと自動同期するか、PdM OS独自に管理するかはTBD。
