<!--
これは架空のサンプルに基づくドライラン記録です。実在の組織・製品・意思決定とは関係ありません。
prompts/run-pilot-core-flow.md の実行結果ログ。docs/workflows/pilot-core-flow.md のドライラン実施記録。
-->

# ドライラン記録: run-pilot-core-flow（メカニクス確認）

## 前提・スコープ

【事実】PdM/POに実施可否を確認した結果、以下が確認された（2026-07-23時点）。

- 対象実案件: まだ具体的な案件がない
- このパイロットで検索してよい正本システム: まだ無い（現時点でNotion/Confluence/Jira/GitHubへの実アクセス手段はこのセッションになく、Google Driveは接続済みだが本パイロットでの検索許可は得ていない）
- Work Item ID: Claude Codeに仮採番を依頼された

【決定】上記の前提のもと、本ドライランは以下のスコープで実施する。

- **実データ・実システムへは一切アクセスしない。** 検索・書き込みともに行わない。
- `run-pilot-core-flow.md` / `pilot-core-flow.md` の**手順・成果物契約が機能するか**を検証する目的に限定し、`examples/pilot-feature`（架空サンプル、通知設定のカスタマイズ機能）を素材として流用する。
- 本ドライランの結果は、業務上の決定・承認・実案件の進捗として扱わない。

【決定】Work Item IDは `WI-PILOT-001` を本ドライランの追跡用に仮採番した。ただし内容は既存の架空サンプル（旧ID: `WI-SAMPLE-001` / `SPEC-SAMPLE-001`）を流用しているため、以降の参照は既存IDをそのまま用いる。`WI-PILOT-001` は「このドライランの実施記録そのもの」を指すIDとして扱い、混同しないようにする。ID採番規則自体は [TBD-048](../../docs/decisions/tbd-register.md) のまま未確定。

## 実施内容（run-pilot-core-flow.md の手順との対応）

| # | 手順 | 実施状況 | 備考 |
|---|---|---|---|
| 1 | 知識パック草稿の作成（collect-knowledge.md, deduplication-policy.md準拠） | 実施せず（既存の [knowledge-pack.yaml](knowledge-pack.yaml) を流用） | 実システム検索が許可されていないため、新規検索は行っていない。既存の架空データが `deduplication-policy.md` の形式（`is_current_spec`, `conflict_notes` 等）に沿っているかのみ確認した → 準拠していることを確認 |
| 2 | 仕様書草稿の作成（create-specification.md準拠、FR-001形式のID付与） | 確認のみ（既存の [specification.md](specification.md) は既にFR-001〜FR-003形式で要件IDが付与済み） | 現行のCodexフェーズでの更新により、要件IDの付与は既に本サンプルへ反映されていた |
| 3 | ワイヤーフロー要否の判断・草稿作成 | **新規実施**。FR-001がユーザー操作画面を伴うため「必要」と判断し、[wireflow.md](wireflow.md) を新規作成した | 判断根拠は仕様書の機能要件のみ。画面遷移の詳細（通知種別の粒度等）は新規のオープンクエスチョンとして記録した |
| 4 | 未確定の業務ルール・矛盾・出所不明情報のTBD列挙 | 実施済み。[specification.md](specification.md) の Open Questions に1件追加（通知種別の粒度） | 新たな矛盾は検出されなかった（既存の knowledge-pack.yaml 内の conflict_notes 以外に新規矛盾なし） |
| 5 | Jiraタスク草稿の作成（decompose-tasks.md準拠） | **実施しない。** PdM/POから「仕様書は承認済み」という明示がないため、承認待ちとしてここで停止する | 仕様書ステータスは引き続き `draft`。Jiraタスク草稿化はこのドライランの範囲外 |

## 成果物一覧と正本への参照

| 成果物 | ファイル | 入力 | 出力 | 正本 | 未解決TBD |
|---|---|---|---|---|---|
| 要求・要望記録 | [input.md](input.md) | ステークホルダー発話（架空） | 要件整理のインプット | 原文の正本・保存先: `TBD` ([TBD-052](../../docs/decisions/tbd-register.md)) | 優先度の判断基準 |
| 知識パック | [knowledge-pack.yaml](knowledge-pack.yaml) | 要件、Notion/Confluence/Jira検索結果（架空） | 仕様書作成のインプット | 各アイテムの正本は `source_system` 参照先（架空URLのため実在しない） | 出所系統のスキーマ表現 ([TBD-047](../../docs/decisions/tbd-register.md)) |
| 仕様書 | [specification.md](specification.md) | 要件、知識パック | ワイヤーフロー・Jiraタスク分解のインプット | 承認後はNotion。現在は `draft` | 反映タイミング、通知種別の粒度、優先度判断基準、2024年見送り理由 |
| ワイヤーフロー | [wireflow.md](wireflow.md)（本ドライランで新規作成） | 仕様書（FR-001） | 仕様書レビュー・Jiraタスク分解（デザインタスク）のインプット | 正式ツール・正本: `TBD` ([TBD-029](../../docs/decisions/tbd-register.md)) | 通知種別の粒度、保存操作の有無、エラー表示の有無 |
| 受領レポート | [acceptance-report.md](acceptance-report.md)（既存、本ドライラン範囲外） | — | — | — | 本ドライランでは更新していない（`delivered` 以降のため対象外） |

## 人間のレビュー・承認が必要な箇所

- [specification.md](specification.md) の内容（背景・機能要件・非機能要件の空欄・Open Questions）はすべて未承認の草稿。PdM/POのレビューが必要。
- [wireflow.md](wireflow.md) は新規作成した草稿であり、特に「通知種別の一覧・粒度」「保存操作の有無」は仕様書側にも記載がないため、PdM/POへの確認が必要。
- Jiraタスク分解は未実施。仕様書承認後にあらためて実施する。

## 実施結果を反映すべきPdM OS設計上の改善点（提案）

このドライランを通じて、以下の設計上のギャップが明らかになった。いずれも業務決定ではなく `TBD` として記録し、[tbd-register.md](../../docs/decisions/tbd-register.md) に追記する。

1. 【提案】`pilot-core-flow.md` の「対象の選定条件」は実案件の存在を前提としており、**実案件も正本アクセス許可も無い状態でメカニクスのみを検証するドライラン**の手順が定義されていなかった。今回はその場で本ドキュメントの形式を即興で決めたが、次回以降のために簡潔なドライラン手順を追記する余地がある。
2. 【提案】ワイヤーフロー要否の判断基準（[templates/wireflow.md](../../templates/wireflow.md) の未確定事項）は「画面操作を伴うか」という単純な基準だけでも実務上は十分機能した。ただし種別粒度のような、仕様書のレビュー段階では気づきにくい論点がワイヤーフロー作成時に新たに見つかった。仕様書とワイヤーフローの作成順序・往復の要否を明文化する余地がある。
3. 【事実】Work Item IDの仮採番（`WI-PILOT-001` 等）と、既存サンプルのID（`WI-SAMPLE-001`）が並存すると混乱しやすいことが分かった。採番規則（[TBD-048](../../docs/decisions/tbd-register.md)）の検討時に、「ドライラン用ID」と「実案件用ID」を区別する命名規則も合わせて検討する余地がある。

## 次のアクション（PdM/PO判断待ち）

- 実際にパイロット対象とする案件を選定する（[pilot-core-flow.md](../../docs/workflows/pilot-core-flow.md) の選定条件を参照）。
- 対象システムへの実アクセス許可（少なくとも1つ以上の正本システム）を明確にする。
- 上記が揃った時点で、あらためて `run-pilot-core-flow.md` の実行プロンプトに実データを入力し、本番のパイロットを開始する。

---

## 第2部: フルパイプライン検証（テスト用仮承認、2026-07-23）

【事実】PdM/POから、ダミーデータでの動作検証をパイプライン全体（Jiraタスク草稿〜リリースノートまで）のスコープで実施する指示があった。

【決定】第1部では「仕様書承認済みの明示がない」ため手順5（Jiraタスク分解）以降を実施しなかった。本パートでは検証範囲を広げるため、**「対応する仕様書はテスト用に仮承認されたものとして扱う」という明示的なテスト信号**を導入する。この仮承認は実際の承認ではなく、[specification.md](specification.md) の `ステータス: draft` は変更していない。以降の成果物には全て「テスト用」「実際の承認ではない」旨を明記した。

### 実施した工程と成果物

| 工程 | 参照プロンプト | 成果物 | 前提としたテスト信号 |
|---|---|---|---|
| Jiraタスク分解 | [decompose-tasks.md](../../prompts/decompose-tasks.md) | [jira-tasks/JT-SAMPLE-001-design.md](jira-tasks/JT-SAMPLE-001-design.md) 〜 [JT-SAMPLE-004](jira-tasks/JT-SAMPLE-004-fr003-default-inheritance.md)（4件） | 仕様書テスト用仮承認 |
| 受領判断 | [review-acceptance.md](../../prompts/review-acceptance.md) | 既存の [acceptance-report.md](acceptance-report.md)（`decision: pending` のまま変更せず） | 「テスト用に仮でaccepted扱い」という注記のみ追加（実ファイルは不変） |
| QA依頼 | [create-qa-request.md](../../prompts/create-qa-request.md) | [qa-request.md](qa-request.md) | 受領がテスト用仮accepted |
| QA結果 | schemas/qa-result.schema.yaml（テンプレートなし） | [qa-result.yaml](qa-result.yaml)（`outcome: passed`、ダミー） | QA依頼が送付された体（実際は未送付） |
| リリースノート | [create-release-note.md](../../prompts/create-release-note.md) | [release-note.md](release-note.md)（識別子 `DRYRUN-2026-07-23`、公開先TBDのまま） | QA結果がテスト用ダミーpassed |

いずれの成果物も、実際のJira登録・QA送付・公開は行っていない。状態遷移（`jira_tasks_created` 以降）も確定させていない。

### 検証を通じて実際に判明した設計ギャップ（新規TBD）

第1部と異なり、本パートは実際に成果物を最後まで作成したことで、机上では気づかなかった具体的なギャップが見つかった。

1. **デザインタスクの受け入れ条件が仕様書の要件IDを参照できないケース** — [JT-SAMPLE-001-design.md](jira-tasks/JT-SAMPLE-001-design.md) はワイヤーフローの画面ID（S2）を参照する必要があったが、`jira-task.schema.yaml` の `acceptance_criteria.requirement_ref` は「FR-001等、仕様書の要件ID」を前提とした説明になっており、画面IDを参照する場合の表現が定義されていなかった。
2. **Jira未登録の草稿同士が依存関係をどう参照するか** — `jira-task.schema.yaml` には草稿自身のID（`jira_issue_key` は登録後にのみ存在）がなく、`dependency_refs` が草稿段階で何を指せばよいか（本ドライランでは便宜上 `JT-SAMPLE-00X` という独自の草稿ID表記を使ったが、これはスキーマで定義された値ではない）。
3. **受領が `pending` のまま後工程を試すときの表現方法** — 実際の受領判断を変更せずに後工程（QA依頼以降）だけをテストする、という今回のような「一部だけ仮定する」検証の型が、既存のプロンプト・スキーマのどこにも想定されていなかった。今回は各成果物に手動で注記したが、恒久的なやり方ではない。

これらは [tbd-register.md](../../docs/decisions/tbd-register.md) にTBD-058〜060として追加する。

### 人間のレビュー・承認が必要な箇所（第2部）

- [jira-tasks/](jira-tasks/) 配下の4件はすべて草稿であり、Jiraへの登録前にPdM/POのレビューが必要。特にJT-SAMPLE-001の所見（画面ID参照の扱い）は確認事項。
- [qa-request.md](qa-request.md) は「テスト用仮accepted」という前提つきの草稿であり、実際の受領判断（[acceptance-report.md](acceptance-report.md) の `pending`）が確定するまで送付してはならない。
- [qa-result.yaml](qa-result.yaml) と [release-note.md](release-note.md) は完全にダミーであり、実際のQA・リリースとは無関係。誤って参照・転用されないよう、ファイル冒頭のコメントで明示している。

### 次のアクション（第2部、PdM/PO判断待ち）

- 上記3件の新規ギャップ（TBD-058〜060）について、Codexフェーズでのスキーマ具体化時に検討するか、Claude Codeフェーズで先に方針を決めるかを判断する。
- 実案件でのパイロット実施は、引き続き第1部の「次のアクション」（対象案件の選定、正本アクセス許可の確定）が前提。
