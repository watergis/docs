---
title: インストール
weight: 20
---

このセクションでは、ベクトルタイルの実装方法についてご説明します。

まず、次のイメージを参照し、ツールキットの全体の構成についてご覧になってください。

## システム構成図
![vectortiles-system-structure](./vectortiles-system-structure.png?width=50pc)

## シーケンス図

{{<mermaid align="center">}}
sequenceDiagram
    participant db as PostGIS
    participant user as User
    participant vt as vt
    participant style as mapbox-stylefiles
    participant mapbox as Mapbox Studio
    participant action as Github Actions
    participant ghpages as gh-pages

    db->>vt: GeoJSON
    Note over vt: tippecanoe
    vt->>user: mbtiles
    
    user->>mapbox: Upload mbtiles
    mapbox->>mapbox: Mapboxスタイルファイル
    Note over mapbox: スタイルファイル編集

    db->>vt: GeoJSON
    Note over vt: スタイルファイルが完成したら
    vt->>action: mbtilesアップロード
    action->>ghpages: ベクトルタイル(pbf/mvt) 
    Note over action: ビルド&デプロイ

    mapbox->>user: MapboxスタイルとSVGのダウンロード
    user->>user: スタイルファイルを編集し、gh-pagesにアップロード
    user->>style: スタイルファイルの生成
    user->>style: スプライトファイルの生成
    style->>ghpages: Mapboxスタイルとスプライトのデプロイ

    user-->>user: Mapbox GL JSでのウェブアプリ開発
    user->>action: HTML/JavaScriptのアップロード
    action->>ghpages: HTML/JavaScript
    Note over action: ビルド&デプロイ
{{< /mermaid >}}

## 次に

いよいよ、次から具体的なベクトルタイルの実装方法について説明していきます。