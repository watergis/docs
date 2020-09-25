---
title: ケニア・ナロックウォーター
weight: 41
---

- [Water Supply Map for Narok Water, KENYA](https://narok.water-gis.com)
- 2020年6月から使用開始

{{< narokwater_map >}}

---
## ナロックウォーターのベクトルタイルのデザイン

### 1. ベクトルタイルのURL
#### ベクトルタイル
```
https://narwassco.github.io/vt/tiles/{z}/{x}/{y}.mvt
```

#### スタイルファイル
- Mapbox Street
```
https://narwassco.github.io/mapbox-stylefiles/street/style.json
```
- Mapbox Satellite
```
https://narwassco.github.io/mapbox-stylefiles/satellite/style.json
```
- UNVT
```
https://narwassco.github.io/mapbox-stylefiles/unvt/style.json
```

#### ライセンス
もし彼らのオープンデータをご使用になりたい場合は次のようなアトリビューションを必ず使ってください。

```
Copyright (c) 2020 Narok Water and Serwerage Services Co, Ltd.
```

### 2. レイヤー一覧

|No|Layer|Geometry Type|Min Zoom|Max Zoom|Remarks|
|---|---|---|---|---|---|
|1|[pipeline](#pipeline)|LineString|10|16|It includes all the types of pipeline, but you may seperate by type of pipe such as main line or secondary line if necessary.|
|2|[meter](#meter)|Point|16|16|It only includes household connections.|
|3|[flowmeter](#flowmeter)|Point|14|16|It only includes flow meters to cover wider range of zoom level than consumer meters.|
|4|[valve](#valve)|Point|15|16|eg. gate valve, sluice valve, air valve, non-return valve, etc.|
|5|[firehydrant](#firehydrant)|Point|15|16|It's firehydrant layer|
|6|[washout](#washout)|Point|15|16|It's washout layer|
|7|[tank](#tank)|Polygon|13|16|Distribution tank layer as `Polygon`. However, you might need to change geometry type to `Point`|
|8|[plant](#plant)|Polygon|10|16|It incudes boundries of Water Treatment Plant and Water Intake|
|9|[parcels](#parcels)|Polygon|16|16|It is polygon of parcels data which was provided by Narok town planning office.|
|10|[parcels_annotation](#parcels_annotation)|Point|16|16|We seperated parcel number from other parcel data due to reducing the size of data.|
|11|[village](#village)|Polygon|10|16|Narok water is zoning some area which is called `village`, you may change layer name for your company.|
|12|[dma](#dma)|Polygon|13|16|District Metered Area(DMA) for Non-Revenue Water Management|
|13|[point_annotation](#point_annotation)|Point|10|16|We put all the annotation data here if we need to show some label.|

ナロックウォーターでは、浄水場の中にポンプ上はありますが、ポンプレイヤーがありません。ただしこれは水道事業体にとっては重要なレイヤーでもあるので、ポンプ上レイヤーも追加しても良いかもしれません。

### 3. 各レイヤーの属性情報
#### pipeline
|No|Column|Data Type|
|---|---|---|
|1| fid |Integer|
|2| pipe_type |String|
|3| pipesize |Integer|
|4| material | String |
|5| constructiondate |Date|
|6| insertdate |Date|
|7| updatedate | Date |
|8| Town | String |

#### meter
|No|Column|Data Type|
|---|---|---|
|1| fid |Integer|
|2| metertype |String|
|3| diameter |String|
|4| zonecd | String |
|5| connno |String|
|6| installationdate |Date|
|7| status | String |
|8| customer | String |
|9| village | String |
|10| insertdate | Date |
|11| updatedate | Date |
|12| isjica | Boolean |

#### flowmeter
|No|Column|Data Type|
|---|---|---|
|1| fid |Integer|
|2| metertype |String|
|3| diameter |String|
|4| zonecd | String |
|5| connno |String|
|6| installationdate |Date|
|7| status | String |
|8| customer | String |
|9| village | String |
|10| insertdate | Date |
|11| updatedate | Date |
|12| isjica | Boolean |

#### valve
|No|Column|Data Type|
|---|---|---|
|1| fid |Integer|
|2| valvetype |String|
|3| diameter |String|
|4| installationdate | Date |
|5| status |String|
|6| insertdate | Date |
|7| updatedate | Date |
|8| isjica | Boolean |

#### firehydrant
|No|Column|Data Type|
|---|---|---|
|1| fid |Integer|
|2| size |String|
|3| installationdate | Date |
|4| insertdate | Date |
|5| updatedate | Date |
|6| isjica | Boolean |

#### washout
|No|Column|Data Type|
|---|---|---|
|1| fid |Integer|
|2| size |String|
|3| installationdate | Date |
|4| insertdate | Date |
|5| updatedate | Date |
|6| isjica | Boolean |

#### tank
|No|Column|Data Type|
|---|---|---|
|1| fid |Integer|
|2| name |String|
|3| capacity | Integer |
|4| servicelocation | String |
|5| material | String |
|6| constructiondate | String |
|7| insertdate | Date |
|8| updatedate | Date |

#### plant
|No|Column|Data Type|
|---|---|---|
|1| fid |Integer|
|2| name |String|
|3| plant_type | String |
|4| insertdate | Date |
|5| updatedate | Date |

#### parcels
|No|Column|Data Type|
|---|---|---|
|1| fid |Integer|
|2| parcel_no |Integer|

#### parcels_annotation
|No|Column|Data Type|
|---|---|---|
|1| fid |Integer|
|2| parcel_no |Integer|

#### village
|No|Column|Data Type|
|---|---|---|
|1| fid |Integer|
|2| name |String|
|3| area |String|
|4| zone |String|
|5| insertdate |Date|
|6| updatedate |Date|

#### dma
|No|Column|Data Type|
|---|---|---|
|1| fid |Integer|
|2| name |String|
|3| insertdate |Date|
|4| updatedate |Date|

#### point_annotation
|No|Column|Data Type|
|---|---|---|
|1| masterid |Integer|
|2| name |String|
|3| layer |String|

`point_annotation` layer contains the following layers' annotation.
- tank
- wtp
- intake
- village
- dma
- places

---
`Copyright © 2020 Narok Water and Sewerage Services Co., Ltd., KENYA`