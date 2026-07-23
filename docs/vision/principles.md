# 設計原則

## 1. 正本 (Source of Truth) は常に単一で、外部システムにある

このリポジトリおよび将来の実装は、正本のコピーを持たない。常に正本システム（Notion / Confluence / Google Drive / Jira / GitHub）を参照し、生成物には参照元へのリンクを残す。詳細は [docs/architecture/source-of-truth.md](../architecture/source-of-truth.md)。

## 2. エージェントは提案し、人間が決定する

要件整理・仕様書草稿・タスク分解・受領判断・QA依頼・リリースノートのいずれも、エージェントは草稿・提案・チェックリストを生成するところまでを担当し、承認・受領・リリース可否の最終判断はPdM/POが行う。詳細は [docs/architecture/approval-policy.md](../architecture/approval-policy.md)。

## 3. 不明な業務ルールは推測せずTBDにする

組織固有の承認者・SLA・優先度基準などは、明示的に確認されるまで `TBD` と記録する。推測で埋めた場合、誤った前提のまま業務が回るリスクの方が、未確定であることの不便さより大きい。

## 4. トレーサビリティを常に保つ

要求・要望 → 要件 → 仕様書 → Jiraタスク → 実装 (GitHub) → 受領判断 → QA依頼 → リリースノート、の各段階が相互にリンクし、どの成果物がどの要件に由来するかを常に辿れるようにする。

## 5. 検索は「今の正しい情報」と「過去の経緯」を区別する

現行仕様 (Notion) と過去仕様 (Confluence) は別の正本として扱い、混同しない。過去資料は「なぜ今の仕様になったか」の経緯を知るために参照し、現行仕様の代わりにはしない。詳細は [docs/architecture/knowledge-routing.md](../architecture/knowledge-routing.md)。

## 6. テンプレート・スキーマは最小から始める

最初から完璧な網羅を狙わず、pilot-feature (examples/) で実際に使ってみて過不足を確認しながら拡張する。

## 7. モデル・ツールに依存しない設計にする

`docs/agents/` で定義するのは機能的な役割であり、特定のAIモデル（Claude, Codex, Gemini等）やツール（Notion AI等）への依存を前提にしない。将来担当ツールが変わっても、業務フロー・状態遷移・責務分担の定義自体は維持できる構造にする。現時点のツールごとの暫定的な役割分担は [docs/agents/ai-tool-roles.md](../agents/ai-tool-roles.md) に切り離して記録する。

## 8. 事実・仮定・提案・決定を区別する

ドキュメント上の記述は、ユーザーが明示した事実、確認が取れていない仮定、Claude/Codexが設計として出す提案、承認・ADRにより確定した決定を混同しない。ラベルの付け方は [AGENTS.md](../../AGENTS.md) を参照。業務上の決定を、エージェントが勝手に確定させない。
