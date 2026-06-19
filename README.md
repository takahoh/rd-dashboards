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

## アクセス制御

- ポータル (`/`) でパスワード認証を行います
- 認証後、同一タブ/セッション内は再入力不要です（`sessionStorage` で管理）
- `/search/` `/einstein/` に直接アクセスした場合、未認証ならポータルにリダイレクトされます
- ブラウザタブを閉じると認証がリセットされます

---

## デプロイ方法

### 初回セットアップ

```bash
cd dashboard-deploy
git init
git add .
git commit -m "Add analytics dashboards"
git remote add origin git@github.com:<username>/<repo>.git
git push -u origin main
```

### GitHub Pages 有効化

1. GitHub でリポジトリを開く
2. **Settings** → **Pages**
3. Source: **Deploy from a branch**
4. Branch: `main` / `/ (root)` を選択
5. **Save**

1〜2分後にURLが有効になります。

### ダッシュボード更新時

元ファイルを編集後、デプロイディレクトリにコピーして push します。

```bash
# 検索ダッシュボード
cp <元パス>/search_conversion_dashboard.html ./search/index.html

# Einstein ダッシュボード
cp <元パス>/einstein_analysis.html ./einstein/index.html

git add .
git commit -m "Update dashboards"
git push
```

push すると自動的に再デプロイされます（通常1分以内）。

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

## セキュリティについて

| レイヤー | 内容 |
|---|---|
| リポジトリ | Private（ソースコード非公開） |
| Pages URL | パスワードゲートで保護 |
| データ | リポジトリ/Pagesには含まれない（ブラウザでローカル読み込み） |
| パスワード保管 | SHA-256 ハッシュのみHTMLに記載（平文なし） |

> **注意:** JSベースのパスワードは開発者ツールで回避可能なため、カジュアルな保護レベルです。機密データはHTML/リポジトリに含まれないため、URLが漏洩してもデータ漏洩のリスクはありません。

---

## 各ダッシュボードの対象データ

### 検索分析 (`/search/`)

ファイル名に `search-conversion_queries_with_results` を含む CSV

```
search-conversion_queries_with_results_2026-01-01_2026-01-31.csv
```

### Einstein (`/einstein/`)

Einstein Recommender のエクスポート CSV

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
