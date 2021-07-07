---
title: パッケージとライブラリ
weight: 50
pre: "<b>5. </b>"
chapter: true
---

### 第5章

この章ではこのオープンソースプロジェクトの一覧をご紹介します。

全てのライブラリは[Github](https://github.com/watergis)にあり、一部を除いて**MIT**ライセンスです。

#### 1. Mapbox GL JSクライアント関係のモジュール

| プラグイン | デモ | 備考 |
|---|---|---|
|[watergis/mapbox-gl-export](https://github.com/watergis/mapbox-gl-export)| [demo](./mapbox-gl-export)|PNGとPDFに出力できるシンプルな印刷用コントロール。|
|[watergis/mapbox-gl-legend](https://github.com/watergis/mapbox-gl-legend)| [demo](./mapbox-gl-legend)|シンプルな凡例を追加するコントロール。|
|[watergis/mapbox-gl-elevation](https://github.com/watergis/mapbox-gl-elevation)| [demo](./mapbox-gl-elevation)|Mapbox GL JSに標高取得ツールを追加します。Terrain RGBタイルセットに依存するプラグインです。|
|[watergis/mapbox-gl-valhalla](https://github.com/watergis/mapbox-gl-valhalla)| [demo](./mapbox-gl-valhalla)|ValhallaのAPIに対応したコントロールを追加するプラグインです。|
|[watergis/mapbox-gl-area-switcher](https://github.com/watergis/mapbox-gl-area-switcher)|[demo](./mapbox-gl-area-switcher)| エリアを簡単に切り替えるシンプルなコントロール|
|[watergis/mapbox-gl-popup](https://github.com/watergis/mapbox-gl-popup)|[demo](./mapbox-gl-popup)| Mapbox GL JSにシンプルなポップアップを追加します|
|[watergis/mapbox-gl-pitch-toggle-control](https://github.com/watergis/mapbox-gl-pitch-toggle-control)|[demo](./mapbox-gl-pitch-toggle-control)| 3Dと2Dを切り替えるシンプルな3Dボタンを追加します|
|[watergis/mapboxgljs-boilerplate](https://github.com/watergis/mapboxgljs-boilerplate)|[demo](./mapboxgljs-boilerplate)| 水道事業体向けにMapbox GL JSの実装を既に行い、全てのカスタマイズされたプラグインを含んだテンプレートです。|
|[watergis/mapbox.photon](https://github.com/watergis/mapbox.photon)|[demo](https://watergis.github.io/mapbox.photon/)| Photonジオコーダーのコントロールを追加するプラグインです。Apache 2.0ライセンスです|

#### 2. ベクトルタイル関係のソフトウェア

| プラグイン | 備考 |
|---|---|
|[watergis/vt-boilerplate](https://github.com/watergis/vt-boilerplate)|PostGISからベクトルタイルを生成しGithubページにデプロイするテンプレート|
|[watergis/postgis2geojson](https://github.com/watergis/postgis2geojson)|PostGISからGeoJSONを生成するモジュール|
|[watergis/postgis2mbtiles](https://github.com/watergis/postgis2mbtiles)|PostGISからmbtilesを生成するモジュール|
|[watergis/postgis2mbtiles-docker](https://github.com/watergis/postgis2mbtiles-docker)|`postgis2mbtiles`モジュールのDocker実装|
|[watergis/mbtiles2pbf](https://github.com/watergis/mbtiles2pbf)|mbtilesをpbf(mvt)ベクトルタイルに変換するモジュール|
|[watergis/postgis2vectortiles](https://github.com/watergis/postgis2vectortiles)|PostGISからpbfベクトルタイルをダイレクトに生成するモジュール|
|[watergis/sprite-creator](https://github.com/watergis/sprite-creator)|SVGアイコンからスプライトファイルを生成するモジュール|
|[watergis/mvt-generator](https://github.com/watergis/mvt-generator)|PostGISから直接ベクトルタイルを１タイルずつ生成するモジュール|

#### 3. EPANET関係のソフトウェア

| プラグイン | 備考 |
|---|---|
|[watergis/geojson2inp](https://github.com/watergis/geojson2inp)|GeoJSONファイルからINPファイルを生成するモジュール|
|[watergis/postgis2inp](https://github.com/watergis/postgis2inp)|PostGISからINPファイルを生成するモジュール|

#### 4. 標高関係のソフトウェア

| プラグイン | 備考 |
|---|---|
|[watergis/dem2terrainrgb](https://github.com/watergis/dem2terrainrgb)|DEMをTerrain RGBのラスタタイルセットに変換するPythonモジュール|
|[watergis/terrain-rgb](https://github.com/watergis/terrain-rgb)| 指定した緯度経度でTerrain RGBのラスタタイルセットから標高を取得するTypescriptのモジュール|

#### 5. Elasticsearch関係のソフトウェア

| プラグイン | 備考 |
|---|---|
|[watergis/es_tileserv](https://github.com/watergis/es_tileserv)|Elasticsearchからベクトルタイルを配信するシンプルなタイルサーバー|
|[watergis/elastic2mvt](https://github.com/watergis/elastic2mvt)|ElasticsearchからMapboxベクトルタイルを生成するNodejsモジュール|