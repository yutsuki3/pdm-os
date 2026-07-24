# ワークフロー: 要求・要望 → 要件整理 → 仕様書

## 目的

ステークホルダーからの要求・要望を整理し、既存資料を踏まえた仕様書・ワイヤーフローに落とし込む。

## 関係者・エージェント

- 入力元: PdM/PO（要求・要望の受け手）
- Knowledge Agent: 現行資料・過去資料の検索
- Specification Agent: 仕様書・ワイヤーフローの草稿作成
- 承認者: PdM/PO単独（要件確定・仕様書承認とも。[approval-policy.md](../architecture/approval-policy.md)）

## 手順

1. **要求・要望の記録**
   PdM/POが [templates/requirement.md](../../templates/requirement.md) を用いて、寄せられた要求・要望を記録する。
   出力: Work Item を `requested` 状態で作成 ([schemas/work-item.schema.yaml](../../schemas/work-item.schema.yaml))。

2. **要件への整理**
   PdM/POが背景・目的・受け入れ条件を明文化し、要件として合意する。承認者はPdM/PO単独で、関係者レビューは必須としない（[approval-policy.md](../architecture/approval-policy.md)）。
   出力: Work Item を `requirement_defined` に遷移。

3. **資料検索**
   Knowledge Agentが [prompts/collect-knowledge.md](../../prompts/collect-knowledge.md) に従い、Notion（現行仕様）・Confluence（過去仕様）・Jira（類似要望）を検索し、[schemas/knowledge-item.schema.yaml](../../schemas/knowledge-item.schema.yaml) 形式の知識パックを生成する。複数システムで同じ情報が重複して見つかった場合の扱いは [deduplication-policy.md](../architecture/deduplication-policy.md) に従う。

4. **仕様書草稿の作成**
   Specification Agentが [prompts/create-specification.md](../../prompts/create-specification.md) に従い、要件と知識パックをもとに [templates/specification.md](../../templates/specification.md) 形式の草稿を作成する。
   Work Item を `spec_drafting` に遷移。

5. **ワイヤーフローの作成**
   必要に応じてFigmaで画面遷移を作成する。画面一覧・詳細遷移の正本はFigmaであり、[templates/wireflow.md](../../templates/wireflow.md) には概要とFigma URLへの参照のみを記載する（二重管理を避ける）。

6. **レビュー・承認**
   Work Item を `spec_review` に遷移し、レビューを経て承認されると `spec_approved` になる。承認者はPdM/PO単独。承認基準は、仕様書テンプレートの必須項目に加え、非機能要件・ワイヤーフロー（必要な場合）が明記済みであること（[approval-policy.md](../architecture/approval-policy.md)）。

7. **Notionへの反映**
   承認された仕様書はNotion（正本）へ反映される。反映方法・ページ構成はTBD ([source-of-truth.md](../architecture/source-of-truth.md))。

## 入力/出力まとめ

| ステップ | 入力 | 出力 |
|---|---|---|
| 記録 | ステークホルダーの発話・依頼 | `templates/requirement.md` を埋めたドキュメント |
| 資料検索 | 要件 | `schemas/knowledge-item.schema.yaml` に基づく知識パック |
| 仕様書草稿 | 要件 + 知識パック | `templates/specification.md` を埋めた草稿 |
| 承認 | 仕様書草稿 | Notion上の承認済み仕様書 |

