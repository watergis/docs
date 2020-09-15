---
title: "GIS for Water"
---

# 水道管理のためのベクタータイル

このウェブサイトはMapboxベクタータイルを水道事業体向けに導入する方法を説明します。

どのようにベクタータイルを導入していくか、そして水道事業体内でどのようにGISデータを共有していくのか、ご説明します。

## なぜベクタータイルなのか?

> Vector tiles make huge maps fast while offering full design flexibility. They are the vector data equivalent of image tiles for web mapping, applying the strengths of tiling — developed for caching, scaling and serving map imagery rapidly — to vector data. (from [Mapbox website](https://docs.mapbox.com/vector-tiles/reference/)).

`ベクタータイル`は現時点で最も人気のある進んだマッピング技術であり、そのデータは非常に軽量で高速であり、柔軟に地図のデザインをすることができます。 

運用コストは一般的にラスタベースの地図配信よりも安価に済みます。

アフリカでは、インターネットの環境が特に地方部ではまだまだ脆弱なところが多いです。このベクタータイルはそういったインターネットが脆弱な環境に最適であり、非常にスムーズに地図をPCやスマホで閲覧できます。

このベクタータイルツールキットのアプローチはGithub pagesを使うのでサーバーが不要であり、自前のサーバー設備などを持つことが困難なアフリカの水道事業体向けに容易に導入可能です。

## ケーススタディ
[ケーススタディ](./casestudies)のページから実際のアフリカの水道事業体での事例についてご覧ください。

## ベクタータイル導入の手順

1. [ベクタータイル導入前の準備作業](./setups/preparation)

2. [ベクタータイルの導入の手順](./setups/installation)

3. [ベクタータイル運用時のコスト](./operation/costs/)

## このオープンソースプロジェクトへのコントリビューション
このベクタータイルツールキットは **Jin IGARASHI**(ご興味がありましたら、私の[ポートフォリオ](https://water-gis.com)をご覧ください)により開発・メンテナンスされています。

ツールに対してフィードバックなどありましたら、Githubのイシューやプルリクエストなどを通してご協力いただければと思います。また、もしアフリカの水道事業体向けのこのGIS活動にご賛同いただけましたら、[Githubスポンサー](https://github.com/sponsors/JinIgarashi)を通してご支援いただければ助かります。
