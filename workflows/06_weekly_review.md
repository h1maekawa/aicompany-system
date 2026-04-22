# ワークフロー06: 週次改善レビュー

## 目的
	週次のパフォーマンスデータを分析し、収益最大化のための改善施策を提案する。

## 入力ファイル
- `workflows/kpi_weekly.csv`
- `workflows/content_queue.csv`
- `workflows/topic_queue.csv`

## 手順

### Step 1: データ集計
1. kpi_weekly.csv の過去4週分のデータを抽出
2. 全記事・全チャネルの指標を集計:
   - PV / sessions
   - CTR（clicks / impressions）
   - CTA CTR（cta_clicks / sessions）
   - CVR（conversions / sessions）
   - EPC（revenue / sessions）
   - revenue（総収益）

### Step 2: 指標計算
| 指標 | 計算式 | 目標値 |
|------|--------|--------|
| CTR | clicks / impressions × 100 | 5%以上 |
| CTA CTR | cta_clicks / sessions × 100 | 3%以上 |
| CVR | conversions / sessions × 100 | 1%以上 |
| EPC | revenue / sessions | ¥50以上 |

### Step 3: 記事をEPC順にソート
1. 全記事をEPC降順でソート
2. 上位3件（勝ち記事）を抽出
3. 下位3件（負け記事）を抽出

### Step 4: 原因分析

#### 勝ち記事の分析
- なぜ这么好的結果だったのか
- タイトル・内容・導線の强みを抽出
- 類似パターンを次回に展开する施策を提案

#### 負け記事の分析
- 何が问题了 причину 分析
- CTR低 / CTA CTR低 / CVR低 のいずれかを特定
- 改善 or 停止の判断

### Step 5: 改善施策の提案

| 記事 | 最も问题の箇所 | 推奨施策 | 優先度 |
|------|---------------|----------|--------|
| ... | CTR低 / CTA CTR低 / CVR低 | ... | 高/中/低 |

### Step 6: topic_queue へのフィードバック
1. 新規テーマに追加すべきものを特定
2. 既存テーマの优先顺位変更を提案
3. Secretary への报告内容を作成

## 週次の判断基準

### 勝利記事の强化
- EPC ¥50以上 → アクセス増加施策
- 类似パターンを新規テーマに展開

### 負け記事の处置
| 状態 | 判断 | 处置 |
|------|------|------|
| EPC < ¥20 持续3週間 | 停止推荐 | 新テーマに切换 |
| CTR < 1% 持续2週間 | 大幅修正 or 停止 | タイトル・内容見直し |
| CVR < 0.5% 持续2週間 | 導線見直し | A8リンク先确认 |

## 出力
1. 週次パフォーマンスサマリー
2. 勝ち記事TOP3 / 負け記事TOP3
3. 改善施策リスト
4. 次週優先順位
5. topic_queue へのフィードバック

## Secretary への報告フォーマット

```
## Analytics Weekly Report — {年月週}

### 週間サマリー
- total_revenue: ¥____
- total_sessions: ____
- avg_epc: ¥____
- winning_articles: N件
- losing_articles: N件

### 即座に采取すべき行動
1. [最も効果が高い施策]
2. [最も问题が大きい箇所の改善]
3. [新規テーマ投入判断]

### 次週優先順位（Secretary確認用）
| 順位 | content_id | 理由 | 期待效果 |
|------|------------|------|----------|
| 1 | ... | ... | ... |
```

## 週次の運用スケジュール
- **毎週月曜日**: Analytics AI起動、前週データ分析
- **午後**: Secretary への報告
- **火曜日**: Secretary 判断 → 各AIへの指示发布