# ワークフロー03: 収益導線組み込み

## 目的
	生成記事の収益導線を最適化し、A8リンクの 配置・CTA・内部リンクを設計する。

## 入力ファイル
- `workflows/content_queue.csv`（draft状態の記事）
- `workflows/offer_registry.csv`
- `workflows/internal_link_map.csv`
- `templates/cta_template.md`

## 手順

### Step 1: 記事分析
1. content_queue.csv から status=draft を抽出
2. 各記事の stage（TOFU/MOFU/BOFU）を確認
3. 関連A8案件を確認

### Step 2: 読者温度判定
| 記事stage | 読者温度 | 最適CTA |
|------------|----------|---------|
| TOFU | コールド | メール登録 / note誘導 |
| MOFU | ミドル | 比較記事誘導 / メール登録 |
| BOFU | ホット | A8リンク直クリック |

### Step 3: CTA 配置設計
| stage | 最大CTA数 | 配置場所 |
|--------|-----------|----------|
| TOFU | 1回 | 本文末尾 |
| MOFU | 2回 | 本文中 + 末尾 |
| BOFU | 3回 | 本文中 + まとめ前 + まとめ直後 |

CTA 配置ルール:
- 1回目: 導入部後の自然発生箇所
- 2回目: まとめ前（比較説明後）
- 3回目: 本文末尾（まとめの中）

### Step 4: 内部リンク配置
1. internal_link_map.csv を確認
2. 各stage間の導線を最低5本設定
3. [INTERNAL_LINK_XXX] プレースホルダを使用

内部リンク配置の優先順位:
- TOFU → MOFU 比較記事
- MOFU → BOFU レビュー記事
- BOFU → A8リンク

### Step 5: A8リンク 配置（BOFUのみ）
1. offer_registry.csv から該当案件を確認
2. [A8_LINK_XXX] プレースホルダをCTAとして使用
3. リンク先が実際の案件と一致することを確認

### Step 6: approval_queue 登録
1. 各記事の承認アイテムを approval_queue.csv に登録
2. checkpoints に以下を設定:
   - CTA配置確認
   - 内部リンク5本以上確認
   - A8リンク先が正しいか確認
3. status = pending