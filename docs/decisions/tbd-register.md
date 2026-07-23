# 未決定事項一覧 (TBD Register)

リポジトリ内に散在する `TBD` をカテゴリ別に集約したもの。新しいTBDを追加・解消した場合は、該当ドキュメントとあわせてこの一覧も更新する。各行の「関連ドキュメント」から詳細を確認できる。

ステータスは以下のいずれか。

- `未着手`: まだ検討されていない
- `検討中`: 部分的に方針はあるが未確定
- `要確認`: ユーザー・関係者への確認が必要

## 1. 正本・情報管理

| ID | 項目 | 内容 | 関連ドキュメント | ステータス |
|---|---|---|---|---|
| TBD-001 | 矛盾の記録先・フォーマット | 正本間の矛盾を検知した際、どこに・どんな形式で記録するか | [deduplication-policy.md](../architecture/deduplication-policy.md), [ADR-0003](ADR-0003-conflict-logging-over-silent-resolution.md) | 未着手 |
| TBD-002 | 矛盾のエスカレーション先・SLA | 記録された矛盾を誰がレビューし、いつまでに解決するか | [source-of-truth.md](../architecture/source-of-truth.md) | 未着手 |
| TBD-003 | 同一出所の機械的判定方法 | 複数のヒットが同じ情報の転記かどうかをどう判定するか | [deduplication-policy.md](../architecture/deduplication-policy.md) | 未着手 |
| TBD-004 | 各正本システムへの検索アクセス手段 | API連携かエクスポートデータの検索か | [knowledge-routing.md](../architecture/knowledge-routing.md) | 未着手 |
| TBD-005 | 検索結果の関連度スコア算出方法 | `relevance_score` の意味・算出方法 | [knowledge-item.schema.yaml](../../schemas/knowledge-item.schema.yaml) | 未着手（Codex検討事項） |
| TBD-006 | 検索範囲の権限制御 | PdM/POが閲覧権限を持たない情報を除外するか | [knowledge-routing.md](../architecture/knowledge-routing.md) | 未着手 |
| TBD-007 | Notionへの仕様書反映方法・タイミング | 承認後、誰が・どう・いつNotionへ反映するか | [source-of-truth.md](../architecture/source-of-truth.md), [specification-agent.md](../agents/specification-agent.md) | 要確認 |
| TBD-008 | 意思決定ログの置き場所・フォーマット | Notion上のどこに「なぜその仕様にしたか」を記録するか | [source-of-truth.md](../architecture/source-of-truth.md) | 未着手 |
| TBD-009 | Confluenceのスペース構成・検索範囲 | 過去仕様がどのスペースに、どこまで遡って存在するか | [source-of-truth.md](../architecture/source-of-truth.md) | 要確認 |

## 2. 承認・権限

| ID | 項目 | 内容 | 関連ドキュメント | ステータス |
|---|---|---|---|---|
| TBD-010 | 要件確定の承認者・基準 | PdM単独か関係者レビューが必要か | [approval-policy.md](../architecture/approval-policy.md) | 要確認 |
| TBD-011 | 仕様書承認の承認者・基準 | PdMのみかエンジニア/デザイナー合意も必須か | [approval-policy.md](../architecture/approval-policy.md) | 要確認 |
| TBD-012 | 受領判断の承認者・基準 | 想定はPdM/POだが確定していない。チェックリスト合格基準も未定 | [approval-policy.md](../architecture/approval-policy.md), [workflows/acceptance.md](../workflows/acceptance.md) | 要確認 |
| TBD-013 | QA依頼送付可否の承認者・基準 | 受領後に必ずQAを挟むか、条件次第でスキップするか | [approval-policy.md](../architecture/approval-policy.md), [workflows/qa-request.md](../workflows/qa-request.md) | 要確認 |
| TBD-014 | リリース可否の承認者・基準 | リリース判定会議の有無・承認フロー | [approval-policy.md](../architecture/approval-policy.md) | 要確認 |
| TBD-015 | 承認に必要な人数・合議の要否 | 各ゲート共通 | [approval-policy.md](../architecture/approval-policy.md) | 未着手 |
| TBD-016 | 承認の記録方法 | Notion上のプロパティか、Jiraのワークフローか | [approval-policy.md](../architecture/approval-policy.md) | 未着手 |
| TBD-017 | 緊急時（ホットフィックス等）の承認簡略化規定 | 例外規定の有無 | [approval-policy.md](../architecture/approval-policy.md) | 未着手 |
| TBD-018 | 優先度の判断基準 | 要求・要望の優先度をどう決めるか | [templates/requirement.md](../../templates/requirement.md) | 要確認 |

## 3. Jira連携

| ID | 項目 | 内容 | 関連ドキュメント | ステータス |
|---|---|---|---|---|
| TBD-019 | プロジェクトキー・課題タイプ体系 | Jira上のプロジェクト構成 | [source-of-truth.md](../architecture/source-of-truth.md), [templates/jira-task.md](../../templates/jira-task.md) | 要確認 |
| TBD-020 | 必須カスタムフィールド | タスク作成時に必須の項目 | [templates/jira-task.md](../../templates/jira-task.md) | 要確認 |
| TBD-021 | タスク分解の粒度基準 | 1画面1タスクか機能単位か | [workflows/spec-to-jira.md](../workflows/spec-to-jira.md), [prompts/decompose-tasks.md](../../prompts/decompose-tasks.md) | 未着手 |
| TBD-022 | 見積りの単位・タイミング | ストーリーポイント/時間、誰がいつ入れるか | [templates/jira-task.md](../../templates/jira-task.md) | 未着手 |
| TBD-023 | デザイン/実装タスクの依存関係表現 | Jira上のリンク種別 | [workflows/spec-to-jira.md](../workflows/spec-to-jira.md) | 未着手 |
| TBD-024 | 複数Jiraタスクの進捗をWork Item状態へ集約する方法 | 1つのWork Itemが複数タスクに分解された場合の集約方法 | [state-machine.md](../architecture/state-machine.md) | 未着手 |

## 4. GitHub実装事実

| ID | 項目 | 内容 | 関連ドキュメント | ステータス |
|---|---|---|---|---|
| TBD-025 | 実装事実の単位 | PR/コミット/リリースタグのどれを単位とするか | [source-of-truth.md](../architecture/source-of-truth.md) | 要確認 |
| TBD-026 | 対象リポジトリの範囲 | 受領判断で参照するGitHubリポジトリの範囲 | [workflows/acceptance.md](../workflows/acceptance.md) | 未着手 |
| TBD-027 | GitHub実装とJira/仕様書の紐付けルール | コミットメッセージ規約・PRテンプレート等 | [acceptance-agent.md](../agents/acceptance-agent.md) | 未着手 |

## 5. Google Drive受領原本

| ID | 項目 | 内容 | 関連ドキュメント | ステータス |
|---|---|---|---|---|
| TBD-028 | 受領原本の特定方法 | フォルダ構成・命名規則・ステータスプロパティ | [source-of-truth.md](../architecture/source-of-truth.md) | 要確認 |

## 6. ワイヤーフロー・デザインツール連携

| ID | 項目 | 内容 | 関連ドキュメント | ステータス |
|---|---|---|---|---|
| TBD-029 | ワイヤーフロー作成の正式ツール・フォーマット | Figma等の利用有無 | [templates/wireflow.md](../../templates/wireflow.md) | 要確認 |
| TBD-030 | テンプレートと外部ツール成果物の同期方法 | 二重管理を避ける方法 | [templates/wireflow.md](../../templates/wireflow.md) | 未着手 |

## 7. QA

| ID | 項目 | 内容 | 関連ドキュメント | ステータス |
|---|---|---|---|---|
| TBD-031 | 受領判断とQA依頼の順序 | QA合格が受領の前提条件か | [workflows/qa-request.md](../workflows/qa-request.md) | 要確認 |
| TBD-032 | QA依頼の送付先・送付方法 | 専用Jiraチケット/フォーム等 | [templates/qa-request.md](../../templates/qa-request.md) | 要確認 |
| TBD-033 | entry/exit criteriaの具体的基準 | QA合否判定基準 | [templates/qa-request.md](../../templates/qa-request.md) | 未着手 |
| TBD-034 | QA不合格時の差し戻し先・再依頼フロー | どの状態に戻すか | [state-machine.md](../architecture/state-machine.md) | 未着手 |

## 8. リリース

| ID | 項目 | 内容 | 関連ドキュメント | ステータス |
|---|---|---|---|---|
| TBD-035 | リリース単位の定義 | バージョニング規則（日次/週次/バージョン番号等） | [templates/release-note.md](../../templates/release-note.md) | 要確認 |
| TBD-036 | リリースノートの公開先・フォーマット | Notion/Confluence/社内Slack/顧客向け等 | [workflows/release-note.md](../workflows/release-note.md) | 要確認 |
| TBD-037 | 公開承認者・基準 | 誰が公開を承認するか | [workflows/release-note.md](../workflows/release-note.md) | 要確認 |
| TBD-038 | 過去のリリースノートのアーカイブ先 | Confluence想定だが未確認 | [workflows/release-note.md](../workflows/release-note.md) | 要確認 |

## 9. AIツール・役割分担

| ID | 項目 | 内容 | 関連ドキュメント | ステータス |
|---|---|---|---|---|
| TBD-039 | Gemini・Notion AIの具体的担当範囲 | 現時点で完全に未定 | [ai-tool-roles.md](../agents/ai-tool-roles.md) | 未着手 |
| TBD-040 | 複数ツールが同一機能的役割を分担する場合の引き継ぎ方法 | フォーマット・整合性確保 | [ai-tool-roles.md](../agents/ai-tool-roles.md) | 未着手 |
| TBD-041 | ツール間で見解が割れた場合の解決ルール | 例: Codexのレビューが既存設計と矛盾する場合 | [ai-tool-roles.md](../agents/ai-tool-roles.md) | 未着手 |

## 10. 状態管理・実行形態

| ID | 項目 | 内容 | 関連ドキュメント | ステータス |
|---|---|---|---|---|
| TBD-042 | Work Itemインスタンスの永続化方法 | DB等、この設計フェーズのスコープ外 | [source-of-truth.md](../architecture/source-of-truth.md), [state-machine.md](../architecture/state-machine.md) | 未着手（次フェーズ以降） |
| TBD-043 | Orchestratorの実行形態 | 常駐サービスか、都度起動のCLIか、Claude Code上のスキルか | [overview.md](../architecture/overview.md) | 未着手 |
| TBD-044 | 各エージェントの実装技術 | LLMモデル・フレームワーク | [overview.md](../architecture/overview.md) | 未着手（次フェーズ以降） |
| TBD-045 | 複数Work Itemの並行処理時の優先順位付け | Orchestratorの調整方法 | [orchestrator.md](../agents/orchestrator.md) | 未着手 |
| TBD-046 | 差し戻し（rejected/qa_failed）時の遷移先 | 常に `in_progress` でよいか、`requirement_defined` に戻すケースがあるか | [state-machine.md](../architecture/state-machine.md) | 未着手 |

## 11. スキーマ・実装（Codexフェーズでの検討事項）

| ID | 項目 | 内容 | 関連ドキュメント | ステータス |
|---|---|---|---|---|
| TBD-047 | 出所系統（オリジンのチェーン）のスキーマ表現 | knowledge-itemに重複・出所関係をどう持たせるか | [deduplication-policy.md](../architecture/deduplication-policy.md), [knowledge-item.schema.yaml](../../schemas/knowledge-item.schema.yaml) | 未着手（Codex検討事項） |
| TBD-048 | 各スキーマのID採番ルール | work-item / specification 等のID体系 | [work-item.schema.yaml](../../schemas/work-item.schema.yaml), [specification.schema.yaml](../../schemas/specification.schema.yaml) | 未着手（Codex検討事項） |
| TBD-049 | 非機能要件の必須項目範囲 | specification.schema.yaml の non_functional_requirements | [specification.schema.yaml](../../schemas/specification.schema.yaml) | 未着手（Codex検討事項） |
| TBD-050 | QA結果の正本システム・結果記録形式 | `qa_passed` / `qa_failed` の根拠となるQA結果をどこに記録・参照するか | [source-of-truth.md](../architecture/source-of-truth.md), [qa-result.schema.yaml](../../schemas/qa-result.schema.yaml) | 要確認 |
| TBD-051 | QA依頼の送付記録の正本 | `qa_requested` を確定する送付済み証跡をどこに残すか | [source-of-truth.md](../architecture/source-of-truth.md), [qa-request.schema.yaml](../../schemas/qa-request.schema.yaml) | 要確認 |
| TBD-052 | 要求・要望原文の正本・保存先 | ステークホルダーの原要求をどこで正本として保持するか | [source-of-truth.md](../architecture/source-of-truth.md), [requirement.schema.yaml](../../schemas/requirement.schema.yaml) | 要確認 |
| TBD-053 | 公開済みリリースノートの正本・アーカイブ先 | `released` の公開証跡と過去ノートをどこで保持するか | [source-of-truth.md](../architecture/source-of-truth.md), [release-note.schema.yaml](../../schemas/release-note.schema.yaml) | 要確認 |
| TBD-054 | 状態遷移履歴の記録先・最小項目 | 誰がいつ何を根拠に状態を確定したかをどこに残すか | [state-machine.md](../architecture/state-machine.md), [work-item.schema.yaml](../../schemas/work-item.schema.yaml) | 要確認 |

## 12. パイロット運用

| ID | 項目 | 内容 | 関連ドキュメント | ステータス |
|---|---|---|---|---|
| TBD-055 | 実案件・正本アクセスが無い状態でのドライラン手順 | `pilot-core-flow.md` は実案件の存在を前提としており、メカニクスのみを検証するドライランの標準手順が未定義 | [pilot-core-flow.md](../workflows/pilot-core-flow.md), [examples/pilot-feature/dry-run-result.md](../../examples/pilot-feature/dry-run-result.md) | 未着手 |
| TBD-056 | 仕様書とワイヤーフロー作成の往復要否 | ワイヤーフロー作成時に仕様書に無い論点（種別粒度等）が新たに見つかった場合の往復ルールが未定義 | [templates/wireflow.md](../../templates/wireflow.md), [prompts/create-specification.md](../../prompts/create-specification.md) | 未着手 |
| TBD-057 | ドライラン用IDと実案件用IDの命名規則 | `WI-PILOT-xxx` のような仮採番と実案件IDの区別方法 | [work-item.schema.yaml](../../schemas/work-item.schema.yaml)（TBD-048関連） | 未着手 |
| TBD-058 | デザインタスクの受け入れ条件がワイヤーフロー画面IDを参照する場合の表現 | `jira-task.schema.yaml` の `requirement_ref` は仕様書の要件ID(FR-001等)のみを想定しており、ワイヤーフローの画面IDを参照する場合の書き方が未定義 | [jira-task.schema.yaml](../../schemas/jira-task.schema.yaml), [examples/pilot-feature/jira-tasks/JT-SAMPLE-001-design.md](../../examples/pilot-feature/jira-tasks/JT-SAMPLE-001-design.md) | 未着手（Codex検討事項） |
| TBD-059 | Jira未登録の草稿タスク同士の依存関係参照方法 | `jira_issue_key` は登録後のみ存在するため、草稿段階の `dependency_refs` が何を指すべきか未定義 | [jira-task.schema.yaml](../../schemas/jira-task.schema.yaml) | 未着手（Codex検討事項） |
| TBD-060 | 一部工程だけを仮定してパイプラインを検証する型の未整備 | 受領判断は実際は`pending`のまま、後工程（QA依頼以降）だけをテスト用に仮定して検証する場合の表現方法が、プロンプト・スキーマのどこにも定義されていない | [examples/pilot-feature/dry-run-result.md](../../examples/pilot-feature/dry-run-result.md) 第2部 | 未着手 |

## 更新履歴

- 初版: このリポジトリのTBDを横断的に集約して作成。
- 追記: `run-pilot-core-flow.md` のメカニクス確認ドライラン（[examples/pilot-feature/dry-run-result.md](../../examples/pilot-feature/dry-run-result.md)）実施に伴い、TBD-055〜057を追加。
- 追記: 同ドライラン第2部（フルパイプライン・ダミー検証、Jiraタスク〜リリースノート）実施に伴い、TBD-058〜060を追加。
