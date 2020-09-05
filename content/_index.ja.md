---
title: "GIS for Water"
---

# 水道管理のためのベクタータイルツールキット

このウェブサイトはMapboxベクタータイルを水道事業体向けに導入する方法を説明します。

どのようにベクタータイルを導入していくか、そして水道事業体内でどのようにGISデータを共有していくのか、ご説明します。
 
## アフリカのベクタータイルベースの水道地図
まず、この[オーバービューマップ](https://watergis.github.io/water-map)はベクタータイルベースの水道システムを全てまとめたものです。地図をズームして、好きなポイントをタップし、ポップアップ内のリンクから詳細な水道マップを閲覧することができます。 

Currently, the below orgainizations joined and are using vectortiles for their daily works.
現在のところ、以下の組織がこのベクタータイルを使用して、日常的に業務に活用しています。
- ケニアの**2水道事業体**と**5つの水道システム**
- ルワンダの**1組織**と**1100+以上の水道システム**

{{< overview_map >}}

## なぜベクタータイルなのか?

> Vector tiles make huge maps fast while offering full design flexibility. They are the vector data equivalent of image tiles for web mapping, applying the strengths of tiling — developed for caching, scaling and serving map imagery rapidly — to vector data. (from [Mapbox website](https://docs.mapbox.com/vector-tiles/reference/)).

`ベクタータイル`は現時点で最も人気のある進んだマッピング技術であり、そのデータは非常に軽量で高速であり、柔軟に地図のデザインをすることができます。 

運用コストは一般的にラスタベースの地図配信よりも安価に済みます。

アフリカでは、インターネットの環境が特に地方部ではまだまだ脆弱なところが多いです。このベクタータイルはそういったインターネットが脆弱な環境に最適であり、非常にスムーズに地図をPCやスマホで閲覧でキアmす。

このベクタータイルツールキットのアプローチはGithub pagesを使うのでサーバーが不要であり、自前のサーバー設備などを持つことが困難なアフリカの水道事業体向けに容易に導入可能です。

## ベクタータイル導入の手順

1. [ベクタータイル導入前の準備作業](./setups/preparation)

2. [ベクタータイルの導入の手順](./setups/installation)

3. [ベクタータイル運用時のコスト](./operation/costs/)

## このオープンソースプロジェクトへのコントリビューション
このベクタータイルツールキットは **Jin IGARASHI**(ご興味がありましたら、私の[ポートフォリオ](https://water-gis.com)をご覧ください)により開発・メンテナンスされています. ツールに対してフィードバックなどありましたら、Githubのイシューやプルリクエストなどを通してご協力いただければと思います。

また、もしアフリカの水道事業体向けのこのGIS活動にご賛同いただけましたら、[Githubスポンサー](https://github.com/sponsors/JinIgarashi)を通してドネーションしていただけたら助かります。
