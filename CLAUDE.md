# AI Company System — 実行ルール

## このリポジトリの目的
A8案件に紐づいたSEO記事をAIで生成し、人間がレビューして手動公開する半自動システム。

## 実行の鉄則
1. 1回の実行で1ジョブのみ行う
2. 必ず workflows/topic_queue.csv と workflows/offer_registry.csv を先に読む
3. 記事生成の保存先は content/blog/ または content/note/
4. 実行後は必ず workflows/content_queue.csv を更新する
5. 実行後は必ず workflows/approval_queue.csv を更新する
6. note投稿・X投稿・分析は明示的な指示があるまで実行しない
7. 誇大表現・断定表現・架空の体験談は絶対に禁止

## ディレクトリの役割
- agents/       → 各AIの役割定義（参照用）
- prompts/      → Clineに渡す実行プロンプト（実行用）
- templates/    → 記事生成のフォーマット定義
- workflows/    → CSV台帳とワークフロー定義
- content/blog/ → SEO記事の生成物
- content/note/ → note記事の生成物
- scripts/      → 将来の自動化スクリプト（Lv2以降）
- logs/         → 実行ログ（Lv2以降）
- docs/roles/   → 役割定義ファイル（参照のみ）

## MVPスコープ（今やること）
- topic_queue.csv からテーマ選定
- offer_registry.csv で案件確認
- content/blog/ にSEO記事を生成
- content_queue.csv と approval_queue.csv を更新
- 人間がレビューして手動公開

## MVPスコープ外（やらないこと）
- note自動投稿
- X自動投稿
- KPI自動取得
- LINE通知
