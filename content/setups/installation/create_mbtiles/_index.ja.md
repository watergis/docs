---
title: PostGISからmbtilesを生成する
weight: 22
---

## PostGISからmbtilesを生成する(`vt`で作業します)
- [watergis/postgis2mbtiles](https://github.com/watergis/postgis2mbtiles) : このモジュールは`PostGIS`からデータをGeoJSONで取り出し`mbtiles`を作成します。[mapbox/tippecanoe](https://github.com/mapbox/tippecanoe)を使用しているため、`Windows`環境ではmbtiles生成のためにはDockerを使います。しかし、マシンが`MacOS`や`Ubuntu`の場合は直接モジュールを使うことができます。[watergis/postgis2mbtiles-docker](https://github.com/watergis/postgis2mbtiles-docker)はDockerで実行するためのソースコードです。

まず、`config.js`上でそれぞれのレイヤに対してSQLを作成する必要があります。そうすることで、`postgis2mbtiles`ツールがPostGISから必要なデータを取り出して、mbtilesファイルが生成されます。 

### レイヤに対する基本的な設定
次はPostGISからGeoJSONを取り出す典型的な例です。

```js
{
    name: 'pipeline', //レイヤー名を指定してください。
    geojsonFileName: __dirname + '/pipeline.geojson', //一時的に使用するGeoJSONファイル名を使用してください。
    select: `
    SELECT row_to_json(featurecollection) AS json FROM (
      SELECT
        'FeatureCollection' AS type,
        array_to_json(array_agg(feature)) AS features
      FROM (
        SELECT
          'Feature' AS type,
          ST_AsGeoJSON(ST_MakeValid(x.geom))::json AS geometry,
          row_to_json((
            SELECT t FROM (
              SELECT
                14 as maxzoom,
                11 as minzoom
            ) AS t
          )) AS tippecanoe,
          row_to_json((
            SELECT p FROM (
              SELECT
                x.pipe_id as fid,
                x.material,
                x.pipe_size,
                x.pressure,
                x.construction_year,
                x.rehabilitation_year,
                x.input_date
            ) AS p
          )) AS properties
        FROM pipeline x
        WHERE NOT ST_IsEmpty(x.geom)
      ) AS feature
    ) AS featurecollection
    `
}
```

最小・最大ズームレベルを設定可能な特別な`tippecanoe`用の設定項目があります。

```sql
row_to_json((
  SELECT t FROM (
    SELECT
      14 as maxzoom,
      11 as minzoom
  ) AS t
)) AS tippecanoe,
```

もし座標系が`EPSG:4326`(WGS84)でない場合は、次のようなSQLで座標変換をしなければなりません。

```sql
ST_TRANSFORM(geom,4326)
```

## ユースケース
自身のデータベース用のSQLを作ることは、非常に重要なステップです。しかし、場合によってはこれは困難な作業になるかもしれません。次の水道事業体での設定方法の事例などが参考になるかもしれません

- `Narok Water and Sewerage Services Co., Ltd, KENYA` : [config.js](https://github.com/narwassco/vt/blob/master/config.js)
- `Water and Sanitation Corporation, Ltd, RWANDA` : [config.js](https://github.com/WASAC/vt/blob/master/config.js)
- `Nakuru Water and Sanitation Services Co., Ltd, KENYA` : [config.js](https://github.com/nakuruwater/vt/blob/master/config.js)

このアプローチはSQL言語を使って直接PostGISからデータを取り出すので、ほとんど全ての水道事業体のGISデータベースに柔軟に対応することができます。

### ベクトルタイルのデザインの例

ベクトルタイルのデザインをどうするかはGISデータベースの設計とあなたのやりたいことによって変わってきます。次のデザインの例はベクトルタイルを設計する際に参考になるかもしれません。

- [Vectortiles Design for Narok water, Kenya](../../../casestudies/narok)
- [Vectortiles Design for WASAC, Rwanda](../../../casestudies/wasac)