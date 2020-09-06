---
title: インストール
weight: 20
---

このセクションでは、ベクタータイルの実装方法についてご説明します。

まず、次のイメージを参照し、ツールキットの全体の構成についてご覧になってください。

## システム構成図
![vectortiles-system-structure](./vectortiles-system-structure.png?width=50pc)

## シーケンス図

{{<mermaid align="center">}}
sequenceDiagram
    participant db as PostGIS
    participant x as User
    participant a as postgis2mbtiles
    participant b as postgis2vectortiles
    participant d as mapbox-stylefiles
    participant y as Mapbox Studio
    participant z as gh-pages

    db->>a: GeoJSON
    Note over a: tippecanoe
    a->>x: mbtiles
    
    x->>y: mbtilesアップロード
    y->>y: Mapboxスタイル編集
    Note over y: Stylefile editing

    x->>x: postgis2vectortilesの設定変更
    db->>b: GeoJSON
    b->>z: Mapboxベクタータイル(pbf tile) 
    Note over b: gh-pagesへのアップロード

    y->>x: MapboxスタイルとSVGのダウンロード
    x->>x: スタイルファイルを編集し、gh-pagesにアップロード
    x->>d: スタイルファイルの生成
    x->>d: スプライトファイルの生成
    d->>z: Mapboxスタイルとスプライトのアップロード

    x-->>x: Mapbox GL JSでのウェブアプリ開発
    x->>z: HTML/JavaScriptのアップロード
{{< /mermaid >}}

## 次に

いよいよ、次から具体的なベクタータイルの実装方法について説明していきます。