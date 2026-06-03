# Tomo Imai — GIS & Spatial Data Engineer

[🇯🇵 日本語プロフィールはこちら](#日本語プロフィール)

> Turning location data into business insight — PostGIS · Python · QGIS

Based in Japan &nbsp;·&nbsp; Available for freelance projects &nbsp;·&nbsp; English & Japanese

---

## What I Do

I build clean, reproducible geospatial workflows for business problems that involve location — trade area sizing, demographic profiling, route analysis, and site selection.

**Typical deliverables:**
- Spatial analysis using PostGIS and QGIS — from raw data to actionable output
- Python pipelines for government open data ingestion (US Census, Japan e-Stat)
- GIS data processing and format conversion (Shapefile, GeoJSON, CSV)
- OpenStreetMap data extraction and integration
- QGIS-compatible map layers with demographic overlays

I value clear scoping up front and always deliver well-structured, reproducible workflows.

---

## Background

Before freelancing, I spent over 20 years as an engineer in the automotive industry. During this time I worked hands-on with GIS data in navigation map development projects, using QGIS and PostGIS to inspect, process, and analyze real-world geospatial datasets.

That industry background means I am comfortable handling production-level data, coordinating across teams, and delivering to specification.

---

## Portfolio

### 🇺🇸 [GIS Trade Area Analysis — US](https://github.com/TomoImai-GIS/gis-trade-area-analysis-us)

County-level spatial analysis toolkit for the United States.

- PostGIS SQL templates: population density, elderly rate choropleth, route analysis
- Python pipelines for TIGER/Line boundaries + ACS 5-year estimates + Decennial Census 2020
- Covers ~3,221 counties nationwide

<table>
<tr>
  <td width="40%"><a href="https://github.com/TomoImai-GIS/gis-trade-area-analysis-us/blob/master/README.md"><img src="https://raw.githubusercontent.com/TomoImai-GIS/gis-trade-area-analysis-us/master/output/sql/03-02_population_density_county_wide.png" width="100%"/></a><br><sub>Population density by county — contiguous US</sub></td>
  <td width="40%"><a href="https://github.com/TomoImai-GIS/gis-trade-area-analysis-us/blob/master/README.md"><img src="https://raw.githubusercontent.com/TomoImai-GIS/gis-trade-area-analysis-us/master/output/sql/02-05_list_counties_along_route_from_gps_log.png" width="100%"/></a><br><sub>Counties along route — Empire State Bldg → US Capitol (I-95)</sub></td>
</tr>
</table>

### 🇯🇵 [GIS Trade Area Analysis — Japan](https://github.com/TomoImai-GIS/gis-trade-area-analysis)

Municipality-level spatial analysis toolkit for Japan.

- 15 PostGIS SQL templates: trade area population, delivery zone assignment, route analysis
- e-Stat census data integration · 1,917 municipalities
- Python GIS utility library (JIS mesh codes, DMS conversion, Japan Plane Rectangular)

<table>
<tr>
  <td width="40%"><a href="https://github.com/TomoImai-GIS/gis-trade-area-analysis"><img src="https://raw.githubusercontent.com/TomoImai-GIS/gis-trade-area-analysis/master/output/sql/03-02_population_density_choropleth_wide.png" width="100%"/></a><br><sub>Population density by municipality — nationwide (Japan)</sub></td>
  <td width="40%"><a href="https://github.com/TomoImai-GIS/gis-trade-area-analysis/blob/master/docs/analysis/01-03_urban_aging_dynamics.md"><img src="https://raw.githubusercontent.com/TomoImai-GIS/gis-trade-area-analysis/master/output/python/01-03_scatter_shift.png" width="100%"/></a><br><sub>Urban aging dynamics 2015→2020 — shift vectors by municipality type</sub></td>
</tr>
</table>

---

## Tools & Stack

![PostgreSQL](https://img.shields.io/badge/PostgreSQL-12%2B-336791?logo=postgresql&logoColor=white)
![PostGIS](https://img.shields.io/badge/PostGIS-3.0%2B-4CAF50)
![Python](https://img.shields.io/badge/Python-3.9%2B-3776AB?logo=python&logoColor=white)
![QGIS](https://img.shields.io/badge/QGIS-3.x-589632?logo=qgis&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-150458?logo=pandas&logoColor=white)
![OpenStreetMap](https://img.shields.io/badge/OpenStreetMap-7EBC6F?logo=openstreetmap&logoColor=white)

---

## Availability

- Remote &nbsp;·&nbsp; English & Japanese
- **Upwork:** [View profile & hire](https://www.upwork.com/freelancers/~014a6e817000929a69)

---

## 日本語プロフィール

PostGIS・Python・QGISを使った空間データ分析のフリーランス案件を承っています。

**得意分野：**
- 商圏分析・人口統計分析（国勢調査・ACSデータ活用）
- GISデータの処理・クリーニング・フォーマット変換（Shapefile、GeoJSON等）
- OpenStreetMapデータの抽出・加工
- 政府オープンデータの取り込みパイプライン構築（e-Stat・US Census）
- QGISによるコロプレスマップ出力

**経歴：**
前職では自動車業界にて長年エンジニアとして勤務し、車載ナビゲーション地図データの開発に携わりながらQGISとPostGISを業務で使用してきました。

**ポートフォリオ：**
- [分析サンプル・実績まとめ（日本語）](showcase-ja.md) — ユースケース別に画像・SQLサンプル付きで紹介
- [🇺🇸 US版（郡レベル空間分析）](https://github.com/TomoImai-GIS/gis-trade-area-analysis-us)
- [🇯🇵 日本版（市区町村レベル空間分析）](https://github.com/TomoImai-GIS/gis-trade-area-analysis)

**クラウドワークス：** [プロフィールを見る](https://crowdworks.jp/public/employees/6744562)
