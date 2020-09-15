---
title: Mapboxスタイルファイルとスプライトファイルのgh-pagesへのデプロイ
weight: 25
---

## Mapboxスタイルファイルとスプライトファイルのgh-pagesへのデプロイ
- [watergis/sprite-creater](https://github.com/watergis/sprite-creator) : このモジュールがアイコンからスプライトファイルを作ってくれます。 

- `mapbox-stylefiles`という名前のリポジトリを作成してください。 その上で次のような構成でスタイルファイルとスプライトファイルを配置します。

```
|- docs
 |- satellite
  |- sprite
   |- sprite.json
   |- sprite.png
   |- sprite@2x.json
   |- sprite@2x.png
   |- sprite@4x.json
   |- sprite@4x.png
  |- style.json
 |- street
  |- sprite
   |- sprite.json
   |- sprite.png
   |- sprite@2x.json
   |- sprite@2x.png
   |- sprite@4x.json
   |- sprite@4x.png
  |- style.json
|- src
 |- config.js
 |- sprite-create.js
```

### ユースケース
次のようなユースケースがあります。それらのいくつかをフォークして必要に応じて変えていくと良いかもしれません。
- `Narok Water and Sewerage Services Co., Ltd, KENYA` : [narwassco/mapbox-stylefiles](https://github.com/narwassco/mapbox-stylefiles)
- `Water and Sanitation Corporation, Ltd, RWANDA` : [WASAC/mapbox-stylefiles](https://github.com/WASAC/mapbox-stylefiles)
- `Nakuru Water and Sanitation Services Co., Ltd, KENYA` : [nakuruwater/mapbox-stylefiles](https://github.com/nakuruwater/mapbox-stylefiles)

## アイコンからスプライトファイルを作成する

スプライトファイルは[mapbox/maki](https://github.com/mapbox/maki)アイコンと[water-icons](https://github.com/narwassco/water-icons)アイコンから作成され、このリポジトリの`docs`フォルダ配下にできます。`UNVT`のベースマップは`mapbox/maki`アイコンを使っています。`ナロックウォーター`のケースでは次のリポジトリでスタイルファイルで使われるアイコンを管理しています。
  - [narwassco/water-icons](https://github.com/narwassco/water-icons) : 水道施設ようにカスタマイズされたアイコンを含みます。
  - [narwassco/mapbox-street-icons](https://github.com/narwassco/mapbox-street-icons) : Mapbox Streetスタイルのアイコンを含みます。
  - [narwassco/mapbox-satellite-icons](https://github.com/narwassco/mapbox-satellite-icons):Mapbox Satelliteスタイルのアイコンを含みます。

## Mapboxスタイルファイルを配置する

Mapbox StudioからMapboxスタイルファイルをダウンロードした後、そのスタイルファイルから不要なコンテンツを削除し、`ベクタータイル`と`スプライトファイル`のURLを変更します。

特に、次の`sources`、`sprite`と`glyphs`のプロパティは必ず変更しなければなりません。
```json
"sources": {
    "composite": {
        "url": "mapbox://mapbox.mapbox-streets-v8,mapbox.mapbox-terrain-v2",
        "type": "vector"
    },
    "assets": {
        "attribution": "©NARWASSCO,Ltd.",
        "minzoom": 10,
        "maxzoom": 16,
        "tiles": [
            "https://narwassco.github.io/vt/tiles/{z}/{x}/{y}.mvt"
        ],
        "type": "vector"
    }
},
"sprite": "https://narwassco.github.io/mapbox-stylefiles/street/sprite/sprite",
"glyphs": "mapbox://fonts/narwassco/{fontstack}/{range}.pbf",
```

それから`layers`プロパティの中の`source`の名前も変更します。
```json
{
    "id": "intake",
    "type": "fill",
    "source": "assets",
    "source-layer": "plant",
    "minzoom": 10,
    "filter": ["match", ["get", "plant_type"], ["INTAKE"], true, false],
    "layout": {},
    "paint": {
        "fill-color": "hsl(0, 18%, 85%)",
        "fill-outline-color": "hsl(0, 8%, 6%)",
        "fill-opacity": 0.6
    }
}
```