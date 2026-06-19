# RD Analytics Dashboard

SFCC 検索レポートおよび Einstein Recommender のパフォーマンスを可視化・分析するダッシュボードツール集です。  
GitHub Pages でホスティングし、ブラウザ上で動作します。サーバー不要・データはローカルCSV読み込みのみで完結します。

---

## URL構成

| パス | 内容 |
|---|---|
| `/` | パスワードゲート + ポータル |
| `/search/` | 検索ワード別 Conversion 推移ダッシュボード |
| `/einstein/` | Einstein Recommender パフォーマンスダッシュボード |

---

## リポジトリ構成

```
├── .gitignore
├── README.md
├── index.html              (ポータル + 認証ゲート)
├── search/
│   └── index.html          (検索分析ダッシュボード)
└── einstein/
    └── index.html          (Einstein分析ダッシュボード)
```

---

## 各ダッシュボードの対象データ

**月単位のエクスポートCSVが必要です。** 月ごとにエクスポートしたCSVファイルを複数読み込むことで時系列比較が可能になります。

### 検索分析 (`/search/`)

ファイル名に `search-conversion_queries_with_results` を含む月次CSV

```
search-conversion_queries_with_results_2026-01-01_2026-01-31.csv
search-conversion_queries_with_results_2026-02-01_2026-02-28.csv
```

ファイル名に含まれる日付範囲（`YYYY-MM-DD_YYYY-MM-DD`）から期間を自動取得します。

### Einstein (`/einstein/`)

ファイル名に `recs-perf-by-recom` を含む月次CSV

```
recs-perf-by-recom_2026-01-01_2026-01-31.csv
recs-perf-by-recom_2026-02-01_2026-02-28.csv
```

---

## 機能一覧

### 検索分析ダッシュボード

| タブ | 機能 |
|---|---|
| 推移グラフ | 検索ワード別の指標（CV率・検索数等）を月次折れ線で表示 |
| 異常検知 | 前月比 ±30% 以上の変動ワードを自動抽出 |
| 集計テーブル | 全期間サマリー（平均/最大/最小 CV率、変動幅） |
| RAWデータ | 読み込んだCSVの元データを期間単位で閲覧 |
| インサイト | 4象限マトリクス（クリック率×CV率）+ ファネル分解 |
| 成長/衰退 | 線形トレンドの傾きで成長・衰退ワードをランキング |

### Einstein ダッシュボード

レコメンダー別の月次パフォーマンス分析・スロット比較

---

## 動作環境

- Chrome / Edge 推奨
- インターネット接続が必要（Chart.js を CDN から読み込み）

---

## 機能要望・改善

機能要望やバグ報告は Issue で起票してください。Pull Request も歓迎です。
