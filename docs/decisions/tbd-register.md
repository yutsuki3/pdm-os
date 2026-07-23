# 未決定事項一覧 (TBD Register)

リポジトリ内に散在する `TBD` をカテゴリ別に集約したもの。新しいTBDを追加・解消した場合は、該当ドキュメントとあわせてこの一覧も更新する。各行の「関連ドキュメント」から詳細を確認できる。

ステータスは以下のいずれか。

- `未着手`: まだ検討されていない
- `検討中`: 部分的に方針はあるが未確定
- `要確認`: ユーザー・関係者への確認が必要
- `実案件未検証`: Schema・テンプレート上の定義は追加済みで、ダミーデータでの再現も確認できているが、実案件・実システムでの運用検証がまだ行われていない
- `解決`: ユーザーとの確認により内容が確定した

## 1. 正本・情報管理

| ID | 項目 | 内容 | 関連ドキュメント | ステータス |
|---|---|---|---|---|
| TBD-001 | 矛盾の記録先・フォーマット | 【決定】このリポジトリ側で記録（Work Item付随の矛盾ログ、knowledge-itemのconflict_notes等）。具体的なスキーマ表現は別途TBD | [deduplication-policy.md](../architecture/deduplication-policy.md), [ADR-0003](ADR-0003-conflict-logging-over-silent-resolution.md) | 解決 |
| TBD-002 | 矛盾のエスカレーション先・SLA | 【決定】PdM/POが検知から1週間以内を目安に解決する | [deduplication-policy.md](../architecture/deduplication-policy.md), [source-of-truth.md](../architecture/source-of-truth.md) | 解決 |
| TBD-003 | 同一出所の機械的判定方法 | 複数のヒットが同じ情報の転記かどうかをどう判定するか | [deduplication-policy.md](../architecture/deduplication-policy.md) | 未着手（Codex検討事項） |
| TBD-004 | 各正本システムへの検索アクセス手段 | API連携かエクスポートデータの検索か | [knowledge-routing.md](../architecture/knowledge-routing.md) | 未着手 |
| TBD-005 | 検索結果の関連度スコア算出方法 | `relevance_score` の意味・算出方法 | [knowledge-item.schema.yaml](../../schemas/knowledge-item.schema.yaml) | 未着手（Codex検討事項） |
| TBD-006 | 検索範囲の権限制御 | PdM/POが閲覧権限を持たない情報を除外するか | [knowledge-routing.md](../architecture/knowledge-routing.md) | 未着手 |
| TBD-007 | Notionへの仕様書反映方法・タイミング | 【決定】承認後、PdM/POが手動で反映する。将来的な自動反映は想定するがAPI連携は本フェーズのスコープ外。ページ構成の詳細は別途TBD | [source-of-truth.md](../architecture/source-of-truth.md), [specification-agent.md](../agents/specification-agent.md) | 解決 |
| TBD-008 | 意思決定ログの置き場所・フォーマット | 【決定】仕様書ページ内に「決定理由」セクションを設けて記録する | [source-of-truth.md](../architecture/source-of-truth.md) | 解決 |
| TBD-009 | Confluenceのスペース構成・検索範囲 | 【決定】全スペース・全期間を検索対象とする | [source-of-truth.md](../architecture/source-of-truth.md) | 解決 |

## 2. 承認・権限

| ID | 項目 | 内容 | 関連ドキュメント | ステータス |
|---|---|---|---|---|
| TBD-010 | 要件確定の承認者・基準 | 【決定】承認者はPdM/PO単独（関係者レビュー不要）。基準は背景・目的・受け入れ条件の明文化 | [approval-policy.md](../architecture/approval-policy.md) | 解決 |
| TBD-011 | 仕様書承認の承認者・基準 | 【決定】承認者はPdM/PO単独。基準は必須項目に加え非機能要件・ワイヤーフロー（必要な場合）の明記 | [approval-policy.md](../architecture/approval-policy.md) | 解決 |
| TBD-012 | 受領判断の承認者・基準 | 【決定】承認者はPdM/PO単独。基準は仕様書の要件充足。見た目・文言レベルの差異は軽微として記録の上で受領・フォローアップ、機能・動作に影響する差異は重大として差し戻す | [approval-policy.md](../architecture/approval-policy.md), [workflows/acceptance.md](../workflows/acceptance.md) | 解決 |
| TBD-013 | QA依頼送付可否の承認者・基準 | 【決定】承認者はPdM/PO単独。受領後は例外なく常にQAを通す（条件付きスキップなし） | [approval-policy.md](../architecture/approval-policy.md), [workflows/qa-request.md](../workflows/qa-request.md) | 解決 |
| TBD-014 | リリース可否の承認者・基準 | 【決定】承認者は会議体（PdM/PO + エンジニアリード + QAリード）。基準はQA合格 + リリースノート内容確認 + リスク確認 | [approval-policy.md](../architecture/approval-policy.md) | 解決 |
| TBD-015 | 承認に必要な人数・合議の要否 | 【決定】要件確定・仕様書承認・受領判断・QA依頼送付可否はPdM/PO単独。リリース可否のみ3者の会議体 | [approval-policy.md](../architecture/approval-policy.md) | 解決 |
| TBD-016 | 承認の記録方法 | 【決定】全ゲート共通でNotion上のプロパティに記録 | [approval-policy.md](../architecture/approval-policy.md) | 解決 |
| TBD-017 | 緊急時（ホットフィックス等）の承認簡略化規定 | 【決定】例外規定は設けない。緊急時も常に通常フローを通す | [approval-policy.md](../architecture/approval-policy.md) | 解決 |
| TBD-018 | 優先度の判断基準 | 【決定】影響度×緊急度のマトリクスで判定 | [templates/requirement.md](../../templates/requirement.md) | 解決 |

## 3. Jira連携

| ID | 項目 | 内容 | 関連ドキュメント | ステータス |
|---|---|---|---|---|
| TBD-019 | プロジェクトキー・課題タイプ体系 | Jira上のプロジェクト構成。既に決まっており、ユーザーが具体値を別途共有予定 | [source-of-truth.md](../architecture/source-of-truth.md), [templates/jira-task.md](../../templates/jira-task.md) | 要確認 |
| TBD-020 | 必須カスタムフィールド | タスク作成時に必須の項目。既に決まっており、ユーザーが具体値を別途共有予定 | [templates/jira-task.md](../../templates/jira-task.md) | 要確認 |
| TBD-021 | タスク分解の粒度基準 | 【決定】機能単位（仕様書の機能要件単位） | [workflows/spec-to-jira.md](../workflows/spec-to-jira.md), [prompts/decompose-tasks.md](../../prompts/decompose-tasks.md) | 解決 |
| TBD-022 | 見積りの単位・タイミング | 【決定】ストーリーポイント。担当エンジニア/デザイナーがJira登録後に入力 | [templates/jira-task.md](../../templates/jira-task.md) | 解決 |
| TBD-023 | デザイン/実装タスクの依存関係表現 | 【決定】Jira標準の "Blocks" / "is blocked by" リンクを使用 | [workflows/spec-to-jira.md](../workflows/spec-to-jira.md) | 解決 |
| TBD-024 | 複数Jiraタスクの進捗をWork Item状態へ集約する方法 | 【決定】全タスクが `Done` になった時点で `delivered` へ遷移 | [state-machine.md](../architecture/state-machine.md) | 解決 |

## 4. GitHub実装事実

| ID | 項目 | 内容 | 関連ドキュメント | ステータス |
|---|---|---|---|---|
| TBD-025 | 実装事実の単位 | 【決定】リリースタグを単位とする | [source-of-truth.md](../architecture/source-of-truth.md) | 解決 |
| TBD-026 | 対象リポジトリの範囲 | 【決定】対象Work ItemにJiraタスクで紐付いた特定のリポジトリのみ | [workflows/acceptance.md](../workflows/acceptance.md) | 解決 |
| TBD-027 | GitHub実装とJira/仕様書の紐付けルール | 【決定】コミット/PRにJira課題キー（例: `PROJ-123`）を含める規約 | [acceptance-agent.md](../agents/acceptance-agent.md) | 解決 |

## 5. Google Drive受領原本

| ID | 項目 | 内容 | 関連ドキュメント | ステータス |
|---|---|---|---|---|
| TBD-028 | 受領原本の特定方法 | 【決定】ファイル名・ステータスプロパティで判別（フォルダ構造は問わない）。具体的な命名規則・プロパティ値は別途TBD | [source-of-truth.md](../architecture/source-of-truth.md) | 解決 |

## 6. ワイヤーフロー・デザインツール連携

| ID | 項目 | 内容 | 関連ドキュメント | ステータス |
|---|---|---|---|---|
| TBD-029 | ワイヤーフロー作成の正式ツール・フォーマット | Figma等の利用有無 | [templates/wireflow.md](../../templates/wireflow.md) | 要確認 |
| TBD-030 | テンプレートと外部ツール成果物の同期方法 | 二重管理を避ける方法 | [templates/wireflow.md](../../templates/wireflow.md) | 未着手 |

## 7. QA

| ID | 項目 | 内容 | 関連ドキュメント | ステータス |
|---|---|---|---|---|
| TBD-031 | 受領判断とQA依頼の順序 | 【決定】受領判断が先。受領（accepted）した機能は例外なく常にQAを通す（TBD-013と同一） | [approval-policy.md](../architecture/approval-policy.md), [workflows/qa-request.md](../workflows/qa-request.md) | 解決 |
| TBD-032 | QA依頼の送付先・送付方法 | 【決定】チャットツール（例: Slack）でQAチームへ直接依頼 | [templates/qa-request.md](../../templates/qa-request.md) | 解決 |
| TBD-033 | entry/exit criteriaの具体的基準 | 【決定】Entry: 受領済みでテスト環境にデプロイ済み。Exit: 仕様書の受け入れ条件を全件テスト済みでバグなし | [templates/qa-request.md](../../templates/qa-request.md) | 解決 |
| TBD-034 | QA不合格時の差し戻し先・再依頼フロー | 【決定】常に `in_progress` に戻し、同じJiraタスクで再提出を待つ。再依頼条件の詳細は別途TBD | [state-machine.md](../architecture/state-machine.md) | 解決 |

## 8. リリース

| ID | 項目 | 内容 | 関連ドキュメント | ステータス |
|---|---|---|---|---|
| TBD-035 | リリース単位の定義 | 【決定】機能単位の随時リリース（QA合格次第、定期バッチなし） | [templates/release-note.md](../../templates/release-note.md) | 解決 |
| TBD-036 | リリースノートの公開先・フォーマット | 【決定】社内向けと顧客向けを別々に作成。具体的なチャネル・フォーマットは別途TBD | [workflows/release-note.md](../workflows/release-note.md) | 検討中 |
| TBD-037 | 公開承認者・基準 | 【決定】TBD-014と同一。会議体（PdM/PO + エンジニアリード + QAリード）が、QA合格 + リリースノート内容確認 + リスク確認を基準に承認 | [approval-policy.md](../architecture/approval-policy.md), [workflows/release-note.md](../workflows/release-note.md) | 解決 |
| TBD-038 | 過去のリリースノートのアーカイブ先 | 【決定】Notion（現行仕様と同じ場所） | [workflows/release-note.md](../workflows/release-note.md) | 解決 |

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
| TBD-046 | 差し戻し（rejected/qa_failed）時の遷移先 | 【決定】常に `in_progress` に戻す。`requirement_defined` / `spec_drafting` へ戻すケースは設けない | [state-machine.md](../architecture/state-machine.md) | 解決 |

## 11. スキーマ・実装（Codexフェーズでの検討事項）

| ID | 項目 | 内容 | 関連ドキュメント | ステータス |
|---|---|---|---|---|
| TBD-047 | 出所系統（オリジンのチェーン）のスキーマ表現 | knowledge-itemに重複・出所関係をどう持たせるか | [deduplication-policy.md](../architecture/deduplication-policy.md), [knowledge-item.schema.yaml](../../schemas/knowledge-item.schema.yaml) | 未着手（Codex検討事項） |
| TBD-048 | 各スキーマのID採番ルール | work-item / specification 等のID体系 | [work-item.schema.yaml](../../schemas/work-item.schema.yaml), [specification.schema.yaml](../../schemas/specification.schema.yaml) | 未着手（Codex検討事項） |
| TBD-049 | 非機能要件の必須項目範囲 | specification.schema.yaml の non_functional_requirements | [specification.schema.yaml](../../schemas/specification.schema.yaml) | 未着手（Codex検討事項） |
| TBD-050 | QA結果の正本システム・結果記録形式 | `qa_passed` / `qa_failed` の根拠となるQA結果をどこに記録・参照するか | [source-of-truth.md](../architecture/source-of-truth.md), [qa-result.schema.yaml](../../schemas/qa-result.schema.yaml) | 要確認 |
| TBD-051 | QA依頼の送付記録の正本 | `qa_requested` を確定する送付済み証跡をどこに残すか | [source-of-truth.md](../architecture/source-of-truth.md), [qa-request.schema.yaml](../../schemas/qa-request.schema.yaml) | 要確認 |
| TBD-052 | 要求・要望原文の正本・保存先 | ステークホルダーの原要求をどこで正本として保持するか | [source-of-truth.md](../architecture/source-of-truth.md), [requirement.schema.yaml](../../schemas/requirement.schema.yaml) | 要確認 |
| TBD-053 | 公開済みリリースノートの正本・アーカイブ先 | 【決定】アーカイブ先はNotion（現行仕様と同じ場所）。公開チャネル（社内/顧客向け）の具体形式は別途TBD | [source-of-truth.md](../architecture/source-of-truth.md), [release-note.schema.yaml](../../schemas/release-note.schema.yaml) | 検討中 |
| TBD-054 | 状態遷移履歴の記録先・最小項目 | 誰がいつ何を根拠に状態を確定したかをどこに残すか | [state-machine.md](../architecture/state-machine.md), [work-item.schema.yaml](../../schemas/work-item.schema.yaml) | 要確認 |

## 12. パイロット運用

| ID | 項目 | 内容 | 関連ドキュメント | ステータス |
|---|---|---|---|---|
| TBD-055 | 実案件・正本アクセスが無い状態でのドライラン手順 | `pilot-core-flow.md` は実案件の存在を前提としており、メカニクスのみを検証するドライランの標準手順が未定義 | [pilot-core-flow.md](../workflows/pilot-core-flow.md), [examples/pilot-feature/dry-run-result.md](../../examples/pilot-feature/dry-run-result.md) | 未着手 |
| TBD-056 | 仕様書とワイヤーフロー作成の往復要否 | ワイヤーフロー作成時に仕様書に無い論点（種別粒度等）が新たに見つかった場合の往復ルールが未定義 | [templates/wireflow.md](../../templates/wireflow.md), [prompts/create-specification.md](../../prompts/create-specification.md) | 未着手 |
| TBD-057 | ドライラン用IDと実案件用IDの命名規則 | `WI-PILOT-xxx` のような仮採番と実案件IDの区別方法 | [work-item.schema.yaml](../../schemas/work-item.schema.yaml)（TBD-048関連） | 未着手 |
| TBD-058 | デザインタスクの受け入れ条件がワイヤーフロー画面IDを参照する場合の表現 | `trace_refs` に `source_type` / `source_ref` / `item_ref` を追加し、仕様書要件（FR-001等）とワイヤーフロー画面（S2等）の両方を参照可能にした。ダミーパイプライン再実行（[validation-run-002.md](../../examples/pilot-feature/validation-run-002.md)、JT-SAMPLE-001）で意図どおり機能することを確認 | [jira-task.schema.yaml](../../schemas/jira-task.schema.yaml), [templates/jira-task.md](../../templates/jira-task.md), [examples/pilot-feature/jira-tasks/JT-SAMPLE-001-design.md](../../examples/pilot-feature/jira-tasks/JT-SAMPLE-001-design.md) | 実案件未検証 |
| TBD-059 | Jira未登録の草稿タスク同士の依存関係参照方法 | `draft_id` と構造化した `dependency_refs` を追加し、草稿段階は `jira_task_draft` + `draft_id`、登録後は `jira_issue` + 課題キーで参照できるようにした。`draft_id` の許容文字と同一草稿リスト内の一意性もSchema・テンプレート・プロンプトに反映済み。採番主体・全体採番規則と実案件での検証は未確定 | [jira-task.schema.yaml](../../schemas/jira-task.schema.yaml), [templates/jira-task.md](../../templates/jira-task.md), [decompose-tasks.md](../../prompts/decompose-tasks.md) | 実案件未検証 |
| TBD-060 | 一部工程だけを仮定してパイプラインを検証する型の未整備 | `validation-run` のSchema・テンプレート・ドライラン用プロンプトを追加し、仮定と実際の記録を併記する形式を定義した。ダミーパイプライン再実行（[validation-run-002.md](../../examples/pilot-feature/validation-run-002.md)）で、テスト前提を一箇所に集約して表現できることを確認 | [validation-run.schema.yaml](../../schemas/validation-run.schema.yaml), [run-validation-dry-run.md](../../prompts/run-validation-dry-run.md), [examples/pilot-feature/validation-run-002.md](../../examples/pilot-feature/validation-run-002.md) | 実案件未検証 |
| TBD-061 | Markdown成果物とSchemaの機械検証方法 | 現行テンプレートは人間が読み書きするMarkdownであり、対応Schemaへの自動検証入力（YAML/JSON、front matter、変換器等）が未定義。今回もvalidation-run-002.mdを含め目視確認のみで、機械検証は行えていない。【提案】テンプレート本文を維持したまま、必要項目だけをYAML front matterへ重複なく構造化し、JSON Schema検証入力にする方式を次の検討候補とする | [artifact-contracts.md](../architecture/artifact-contracts.md), [schemas/](../../schemas/) | 検討中（提案あり・未実装） |

## 更新履歴

- 初版: このリポジトリのTBDを横断的に集約して作成。
- 追記: `run-pilot-core-flow.md` のメカニクス確認ドライラン（[examples/pilot-feature/dry-run-result.md](../../examples/pilot-feature/dry-run-result.md)）実施に伴い、TBD-055〜057を追加。
- 追記: 同ドライラン第2部（フルパイプライン・ダミー検証、Jiraタスク〜リリースノート）実施に伴い、TBD-058〜060を追加。
- 更新: CodexレビューによりTBD-058〜060の再利用定義を追加。実案件での運用検証が完了するまで検討中とする。TBD-061を追加。
- 更新: 新形式（draft_id / trace_refs / dependency_refs / validation-run）を使ってダミーパイプラインを再実行し（[validation-run-002.md](../../examples/pilot-feature/validation-run-002.md)）、TBD-058〜060の定義がダミーデータ上で機能することを確認。ステータスを`実案件未検証`に統一（実案件・実システムでの運用検証が残タスクであることを明示）。
- 更新: Round 2のCodexレビューにより、`draft_id` の形式・同一草稿リスト内の一意性、検証用仮定の実記録参照必須を定義へ反映。TBD-061に機械検証方式の提案を追記。
- 更新: ユーザーとの確認により承認ポリシー（TBD-010〜017）が確定。[approval-policy.md](../architecture/approval-policy.md)・[state-machine.md](../architecture/state-machine.md)・関連ワークフローに反映し、ステータスを`解決`に変更。
- 更新: ユーザーとの確認により、正本反映・矛盾処理（TBD-001〜002, 007〜009, 031）、受領判断の差し戻し基準・GitHub/Drive特定方法（TBD-012, 025〜028, 034, 046）、Jira連携の一部（TBD-018, 021〜024）、QA・リリースの残り（TBD-032〜033, 035, 037〜038, 053）が確定。関連する `docs/` `templates/` `schemas/` に反映。TBD-019・020（Jiraプロジェクトキー等の具体値）とTBD-036（公開チャネル詳細）はユーザーが別途共有予定のため`要確認`/`検討中`のまま。
