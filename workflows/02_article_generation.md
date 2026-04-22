# ワークフロー02: 記事生成

## 目的
	topic_queue.csv の priority=high テーマから、SEO記事とnote記事を生成する。

## 入力ファイル
- `workflows/topic_queue.csv`
- `workflows/offer_registry.csv`
- `templates/seo_article_template.md`
- `templates/note_article_template.md`

## 手順

### Step 1: テーマ選定
1. topic_queue.csv を開く
2. status=candidate AND priority=high を抽出
3. 上位テーマを1つ選択（scoreが最も高いもの）

### Step 2: A8案件確認
1. 選択したテーマの related_offer_id を確認
2. offer_registry.csv で案件詳細を確認
3. payout / cookie_days / target_keyword_stage を把握

### Step 3: SEO記事生成
1. templates/seo_article_template.md をベースに生成
2. 必須要素:
   - タイトル案3パターン（primary_keyword 포함、32文字以内）
   - メタディスクリプション（170文字以内）
   - 本文（5,000-8,000字）
   - 内部リンクプレースホルダ 5本以上
   - CTA配置（BOFUならA8_LINK配置）

### Step 4: note記事生成
1. templates/note_article_template.md をベースに生成
2. 必須要素:
   - タイトル案3パターン（共感型）
   - 本文（3,000-5,000字）
   - メール登録導線 [MAIL_REGISTER_LINK]
   - 比較記事誘導 [COMPARE_ARTICLE_URL]

### Step 5: content_queue 更新
1. 生成した記事を content_queue.csv に登録
2. 各 статья に対して新規 content_id を付与
3. status = draft、owner = content_ai、deadline = 3日後
4. approval_required = true

## 出力
- SEO記事初稿（Markdown）
- note記事初稿（Markdown）
- content_queue.csv 更新

## 失敗時の分岐

| 状態 | 处置 |
|------|------|
| キーワード不足 | Market AI へ戻し、再選定 |
| 案件との紐付け不明 | Market AI へ戻し、offer_registry確認 |
| 品質不足（文字数不足） | Content AI 内で再生成（最大3回） |
| 3回やってだめ | Secretary へ報告、却下判断を仰ぐ |

## 承認ポイント
- 記事初稿生成後、Md Monetize AI に受け渡し
- CTA配置・内部リンク設計を Monetize AI が実施
- その後、approval_queue.csv に登録