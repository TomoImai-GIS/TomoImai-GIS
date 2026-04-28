# GIS・空間データ分析 ポートフォリオ

> PostGIS × Python × QGIS で「場所」に関わるビジネス課題を解決します

![PostgreSQL](https://img.shields.io/badge/PostgreSQL-12%2B-336791?logo=postgresql&logoColor=white)
![PostGIS](https://img.shields.io/badge/PostGIS-3.0%2B-4CAF50)
![QGIS](https://img.shields.io/badge/QGIS-3.x-589632?logo=qgis&logoColor=white)
![Python](https://img.shields.io/badge/Python-3.9%2B-3776AB?logo=python&logoColor=white)

[![CrowdWorks](https://img.shields.io/badge/CrowdWorks-プロフィールを見る-00a0e9)](https://crowdworks.jp/public/employees/6744562)
[![GitHub](https://img.shields.io/badge/GitHub-TomoImai--GIS-181717?logo=github)](https://github.com/TomoImai-GIS)

---

## 貢献できる分野

以下のようなお悩みに GIS 分析で課題解決のお役に立ちます。

| お悩み | 対応できる分析 |
|--------|---------------|
| 候補地の商圏人口・高齢化率を素早く試算したい | [商圏人口集計 →](#-商圏分析出店立地調査) |
| 複数の倉庫・拠点に配送エリアを自動で割り当てたい | [配送エリア割り当て →](#-配送エリア設計ルート分析) |
| 顧客住所データを地図に落として営業テリトリーを設計したい | [顧客分布集計 →](#-顧客分布営業テリトリー設計) |
| 高齢化・人口減少のトレンドを地図で可視化して経営判断に使いたい | [人口統計分析 →](#-人口統計高齢化分析) |
| GISデータの処理や変換をまとめて依頼したい | [技術スタック →](#技術スタック) |

---

## 日本版ポートフォリオ

PostGIS と e-Stat（国勢調査）を使った市区町村レベルの空間分析ツールキットです。
全国 **1,917 市区町村**（2015・2020 年国勢調査）をカバーしています。

**→ リポジトリ全体はこちら：[gis-trade-area-analysis](https://github.com/TomoImai-GIS/gis-trade-area-analysis)**

---

### 🏪 商圏分析・出店立地調査

**課題：** 候補地から半径 N km 圏内の人口・高齢化率・世帯数を素早く把握したい。フランチャイズの出店判断や医療施設の立地選定に使いたい。

指定した座標と半径を `WITH params AS (...)` に入力するだけで、圏内の市区町村ごとに人口・高齢者数・人口密度・距離を集計します。

```sql
-- sql/02_analysis/02-01_calc_trade_area_population.sql
WITH params AS (
    SELECT
        136.8816 AS center_lon,   -- 名古屋駅
        35.1706  AS center_lat,
        10000    AS radius_m      -- 半径 10 km
)
```

**→ テンプレート詳細：[02-01_calc_trade_area_population.sql](https://github.com/TomoImai-GIS/gis-trade-area-analysis/blob/master/sql/02_analysis/02-01_calc_trade_area_population.sql)**

---

### 👴 人口統計・高齢化分析

**課題：** 高齢化率や人口密度を地図で見える化して、医療・介護施設の出店計画や自治体の財政計画に活用したい。2015〜2020 年の変化トレンドも把握したい。

#### 全国コロプレスマップ（QGIS 出力）

![高齢化率コロプレス — 全国](https://raw.githubusercontent.com/TomoImai-GIS/gis-trade-area-analysis/master/output/sql/03-02_elderly_rate_choropleth_wide.png)
*高齢化率（65歳以上人口比率）を市区町村別に色分け — 全国版*

![人口密度コロプレス — 全国](https://raw.githubusercontent.com/TomoImai-GIS/gis-trade-area-analysis/master/output/sql/03-02_population_density_choropleth_wide.png)
*人口密度（人/km²）を市区町村別に色分け — 全国版*

**→ 生成クエリ：[03-02_generate_choropleth_elderly_rate.sql](https://github.com/TomoImai-GIS/gis-trade-area-analysis/blob/master/sql/03_visualization/03-02_generate_choropleth_elderly_rate.sql)**

#### 人口密度 × 高齢化率 散布図

![人口密度 vs 高齢化率 散布図](https://raw.githubusercontent.com/TomoImai-GIS/gis-trade-area-analysis/master/output/python/01-01_scatter_density_vs_elderly_rate.png)
*全市区町村（2020年国勢調査）。バブルサイズ＝人口、色＝地域区分、破線＝OLSトレンド*

#### 分析レポートサンプル（詳細は各リンク先の英語レポートをご参照ください）

**[① 都市部高齢化ダイナミクス：2015→2020 仮説検証分析](https://github.com/TomoImai-GIS/gis-trade-area-analysis/blob/master/docs/analysis/01-03_urban_aging_dynamics.md)**

東京圏の8自治体を「都心・住宅地・郊外・農村」4グループに分類し、2015〜2020年の人口密度×高齢化率の変化軌跡を追跡。都心は若返り、内郊外は想定より緩やかな高齢化、外郊外は着実な高齢化、農村は人口流出と高齢化が同時進行という四つの異なる軌跡を検証しています。

![都市部高齢化 — 変化軌跡散布図](https://raw.githubusercontent.com/TomoImai-GIS/gis-trade-area-analysis/master/output/python/01-03_scatter_shift.png)
*8自治体の2015→2020変化ベクトル（矢印の向きと長さで変化方向・速度を表示）*

---

**[② 全国高齢化ダイナミクス：3次元コーホート成長率分析](https://github.com/TomoImai-GIS/gis-trade-area-analysis/blob/master/docs/analysis/01-05_nationwide_aging_dynamics.md)**

全国約1,700自治体の年少・生産年齢・高齢人口それぞれの2015→2020成長率を3次元散布図で可視化。「年少人口と生産年齢人口は一体で動く（世帯単位の移動）」「高齢人口はほぼ全自治体でプラス成長（最後に残る）」という構造を発見しています。

![全国高齢化 — 3次元散布図](https://raw.githubusercontent.com/TomoImai-GIS/gis-trade-area-analysis/master/output/python/01-05_3d_age_static.png)
*全国約1,700自治体の年齢3コーホート成長率を3次元プロット*

> 💡 角度を自在に変えて眺めたい方 → [3次元インタラクティブプロットを開く](https://tomoimai-gis.github.io/gis-trade-area-analysis/output/python/01-05_3d_age_interactive.html)

---

**[③ オクタント分類：人口軌跡タイプ別ヒストグラム分析](https://github.com/TomoImai-GIS/gis-trade-area-analysis/blob/master/docs/analysis/01-07_octant_histogram_analysis.md)**

年少・生産年齢・高齢の成長率の符号の組み合わせで自治体を8タイプに分類し、地図上で可視化。全体の69%が「生産年齢・年少減少、高齢増加」という「連鎖的人口縮小」パターンであることを示しています。

![オクタント分類コロプレス — 全国](https://raw.githubusercontent.com/TomoImai-GIS/gis-trade-area-analysis/master/output/sql/03-03_generate_choropleth_octant_growth_wide.png)
*人口軌跡タイプの地理的分布（全国）。都市集積軸と農村部の対比が明確*

---

### 🚚 配送エリア設計・ルート分析

**課題：** 複数の配送拠点に対して各市区町村を「最寄り拠点」に自動割り当てしたい。また、GPSログや経路ウェイポイントから通過した自治体・走行距離を集計したい。

![ルート通過市区町村 — 名古屋→羽田](https://raw.githubusercontent.com/TomoImai-GIS/gis-trade-area-analysis/master/output/sql/02-05c_list_cities_along_route_from_gps_log.png)
*名古屋駅→羽田空港ルートの通過市区町村を順番に色分け表示（QGIS出力）*

**→ テンプレート一覧：[sql/02_analysis/](https://github.com/TomoImai-GIS/gis-trade-area-analysis/tree/master/sql/02_analysis)**
- [02-03_assign_delivery_area.sql](https://github.com/TomoImai-GIS/gis-trade-area-analysis/blob/master/sql/02_analysis/02-03_assign_delivery_area.sql) — 最寄り拠点への自動割り当て
- [02-05b_list_cities_along_route_simple.sql](https://github.com/TomoImai-GIS/gis-trade-area-analysis/blob/master/sql/02_analysis/02-05b_list_cities_along_route_simple.sql) — ウェイポイント指定ルート分析
- [02-05c_list_cities_along_route_from_gps_log.sql](https://github.com/TomoImai-GIS/gis-trade-area-analysis/blob/master/sql/02_analysis/02-05c_list_cities_along_route_from_gps_log.sql) — GPSログからのルート分析

---

### 📦 顧客分布・営業テリトリー設計

**課題：** 顧客住所（緯度経度）を市区町村単位で集計し、国勢調査人口に対する浸透率を算出して営業エリアの優先順位付けをしたい。データ品質チェック（重複・範囲外座標）も同時に行いたい。

**→ テンプレート：[02-02_aggregate_customer_by_city.sql](https://github.com/TomoImai-GIS/gis-trade-area-analysis/blob/master/sql/02_analysis/02-02_aggregate_customer_by_city.sql)**

市区町村ごとの顧客数・浸透率（顧客数 ÷ 人口）を集計します。人口データとの JOIN により、浸透率の低い高ポテンシャルエリアを特定できます。

---

### SQLテンプレート一覧（日本版）

**13本**のテンプレートが即使用可能です。全て `WITH params AS (...)` ブロックを編集するだけで実行できます。

| カテゴリ | 本数 | 内容 |
|----------|------|------|
| [基本操作](https://github.com/TomoImai-GIS/gis-trade-area-analysis/tree/master/sql/01_basic) | 3 | 逆ジオコーディング・都道府県検索・2点間距離 |
| [空間分析](https://github.com/TomoImai-GIS/gis-trade-area-analysis/tree/master/sql/02_analysis) | 8 | 商圏人口集計・顧客集計・配送割り当て・ルート分析・高齢化ランキング |
| [可視化](https://github.com/TomoImai-GIS/gis-trade-area-analysis/tree/master/sql/03_visualization) | 2 | QGISコロプレスマップ用ポリゴン出力 |

**→ テンプレート全索引（サンプルコード付き）：[sql/README.md](https://github.com/TomoImai-GIS/gis-trade-area-analysis/blob/master/sql/README.md)**

---

## 米国版ポートフォリオ

日本版と同様の空間分析ツールキットを米国（郡レベル）向けに構築しています。
海外企業・英語対応案件にも対応可能です。

**→ リポジトリ：[gis-trade-area-analysis-us](https://github.com/TomoImai-GIS/gis-trade-area-analysis-us)**

**カバレッジ：** 全米約3,221郡（ACS 5年推計2022 + Decennial Census 2020）

![米国人口密度コロプレス — 全国](https://raw.githubusercontent.com/TomoImai-GIS/gis-trade-area-analysis-us/master/output/sql/03-02_population_density_county_wide.png)
*郡別人口密度（人/sq mi）— 全米48州。マンハッタンから内陸部への密度勾配が明確*

![米国ルート通過郡 — NY→DC](https://raw.githubusercontent.com/TomoImai-GIS/gis-trade-area-analysis-us/master/output/sql/02-05_list_counties_along_route_from_gps_log.png)
*エンパイアステートビル（NYC）→米国議会議事堂（DC）ルートの通過郡（I-95経由）*

---

## 技術スタック

| 領域 | 使用技術 |
|------|---------|
| **データベース** | PostgreSQL 12+、PostGIS 3.0+（空間クエリ・地理演算） |
| **GIS ソフト** | QGIS 3.x（コロプレスマップ・ルート可視化・レイヤー出力） |
| **プログラミング** | Python 3.9+（pandas, numpy, matplotlib, psycopg2, pyproj） |
| **座標変換** | WGS84 ↔ 平面直角座標系（全19系対応）、JIS X 0410メッシュコード、DMS変換 |
| **データソース（日本）** | e-Stat 国勢調査（2015・2020年）、国土数値情報（行政界ポリゴン） |
| **データソース（米国）** | US Census ACS 5年推計、Decennial Census 2020、TIGER/Line境界データ |
| **空間演算** | ST_DWithin（圏内検索）、ST_Contains（ポイントインポリゴン）、ST_Intersects（ルート交差） |

---

## ご依頼・お問い合わせ

- **CrowdWorks：** [プロフィールページ](https://crowdworks.jp/public/employees/6744562)
- **Upwork（英語対応）：** [プロフィールページ](https://www.upwork.com/freelancers/~014a6e817000929a69)
- **GitHub：** [TomoImai-GIS](https://github.com/TomoImai-GIS)

納品形式・データソースの手配方法など、ご不明な点はお気軽にご相談ください。
