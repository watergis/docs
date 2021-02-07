---
title: WASAC, Rwanda
weight: 42
---

- [Water Supply Map for WASAC RWSS, RWANDA](https://rural.water-gis.com)
- since July 2020.

## Demo

The below is demo image of `Water Supply Map for WASAC RWSS`
![demo_wasac](/images/showcase/demo_wasac.gif?width=50pc)

{{< wasac_map >}}

---
## Vectortiles Design for WASAC, Rwanda
This is the design of vector tiles for WASAC.
You can also see our database design from [here](https://github.com/WASAC/database_documents).

### 1. URL of Vectortiles
#### Vectortiles
```
https://wasac.github.io/vt/tiles/{z}/{x}/{y}.mvt
```

#### Terrain RGB raster tileset
```
https://wasac.github.io/rw-terrain/tiles/{z}/{x}/{y}.png
```

- available zoom level: 5 - 15
- tile size: 512
- it was made from 10m DEM which is owned by WASAC.

#### Stylefiles
- Mapbox Street ([maputnik editor](https://maputnik.github.io/editor?style=https://wasac.github.io/mapbox-stylefiles/street/style.json))
```
https://wasac.github.io/mapbox-stylefiles/street/style.json
```
- Mapbox Satellite ([maputnik editor](https://maputnik.github.io/editor?style=https://wasac.github.io/mapbox-stylefiles/satellite/style.json))
```
https://wasac.github.io/mapbox-stylefiles/satellite/style.json
```
- UNVT ([maputnik editor](https://maputnik.github.io/editor?style=https://wasac.github.io/mapbox-stylefiles/unvt/style.json))
```
https://wasac.github.io/mapbox-stylefiles/unvt/style.json
```
- Terrain ([maputnik editor](https://maputnik.github.io/editor?style=https://wasac.github.io/mapbox-stylefiles/terrain/style.json))
```
https://wasac.github.io/mapbox-stylefiles/terrain/style.json
```
Note. This terrain stylefile can work on Mapbox GL JS v2 only.　Mapbox GL JS v2 now became proprietary software, you may be charged some fee by them.

#### License
If you want to use their open data, please mention their attiribution. 

```
Copyright (c) 2020 Water and Sanitation Corporation, Ltd.
```

### 2. List of Layers

|No|Layer|Min Zoom|Max Zoom|Geometry Type|
|---|---|---|---|---|
|1|[pipeline](#pipeline)|11|14|LineString|
|2|[connection](#connection)|14|14|Point|
|3|[chamber](#chamber)|14|14|Point|
|4|[watersource](#watersource)|12|14|Point|
|5|[reservoir](#reservoir)|12|14|Point|
|6|[pumping_station](#pumping_station)|12|14|Point|
|7|[wss](#wss)|9|14|Polygon|
|8|[wss_annotation](#wss_annotation)|11|15|Point|
|9|[district](#district)|8|14|Polygon|
|10|[district_annotation](#district_annotation)|8|11|Point|
|11|[sector](#sector)|10|14|Polygon|
|12|[sector_annotation](#sector_annotation)|10|14|Point|
|13|[cell](#cell)|13|14|Polygon|
|14|[cell_annotation](#cell_annotation)|13|14|Point|
|15|[village](#village)|14|14|Polygon|
|16|[village_annotation](#village_annotation)|14|14|Point|

### 3. List of Columns for each layers
#### pipeline
|No|Column|Data Type|
|---|---|---|
|1| fid |Integer|
|2| material |String|
|3| pipe_size |Integer|
|4| pressure | String |
|5| construction_year |Integer|
|6| rehabilitation_year |Integer|
|7| input_date | String |

#### connection
|No|Column|Data Type|
|---|---|---|
|1| fid |Integer|
|2| connection_type |String|
|3| no_user |Integer|
|4| water_meter | Boolean |
|5| status | String |
|6| observation | String |
|7| elevation | Integer |
|8| input_date | String |
|9| construction_year | Integer |
|10| rehabilitation_year | Integer |

#### chamber
|No|Column|Data Type|
|---|---|---|
|1| fid |Integer|
|2| chamber_type |String|
|3| chamber_size | String |
|4| material | String |
|5| status | String |
|6| observation | String |
|7| elevation | Integer |
|8| is_breakpressure | Boolean |
|9| chlorination_unit | Boolean |
|10| construction_year | Integer |
|11| rehabilitation_year | Integer |
|12| input_date | String |

#### watersource
|No|Column|Data Type|
|---|---|---|
|1| fid |Integer|
|2| source_type |String|
|3| discharge | Float |
|4| water_meter | Boolean |
|5| status | String |
|6| observation | String |
|7| elevation | Integer |
|8| chlorination_unit | Boolean |
|9| source_protected | Boolean |
|10| construction_year | Integer |
|11| rehabilitation_year | Integer |
|12| input_date | String |

#### reservoir
|No|Column|Data Type|
|---|---|---|
|1| fid |Integer|
|2| reservoir_type |String|
|3| capacity | Float |
|3| material | String |
|4| water_meter | Boolean |
|5| status | String |
|6| observation | String |
|7| elevation | Integer |
|8| is_breakpressure | Boolean |
|9| meter_installation_date | String |
|10| chlorination_unit | Boolean |
|11| construction_year | Integer |
|12| rehabilitation_year | Integer |
|13| input_date | String |

#### pumping_station
|No|Column|Data Type|
|---|---|---|
|1| fid |Integer|
|2| status | String |
|3| head_pump |String|
|4| power_pump | String |
|5| discharge_pump | String |
|6| pump_type | String |
|7| power_source | String |
|8| no_pump | Integer |
|9| kva | String |
|10| no_generator | Integer |
|11| observation | String |
|12| elevation | Integer |
|13| pump_installation_date | String |
|14| meter_installation_date | String |
|15| capacity_antihummber | String |
|16| water_meter | Boolean |
|17| chlorination_unit | Boolean |
|18| installation_antihummer | Boolean|
|19| construction_year | Integer |
|20| rehabilitation_year | Integer |
|21| input_date | String |

#### wss
|No|Column|Data Type|
|---|---|---|
|1| wss_id |Integer|
|2| wss_name |String|
|3| wss_type |String|
|4| status |String|
|5| description |String|

#### wss_annotation
|No|Column|Data Type|
|---|---|---|
|1| wss_id |Integer|
|2| wss_name | String |

#### district
|No|Column|Data Type|
|---|---|---|
|1| dist_id |Integer|

#### district_annotation
|No|Column|Data Type|
|---|---|---|
|1| dist_id |Integer|
|2| district | String |

#### sector
|No|Column|Data Type|
|---|---|---|
|1| sect_id |Integer|

#### sector_annotation
|No|Column|Data Type|
|---|---|---|
|1| sect_id |Integer|
|2| sector | String |

#### cell
|No|Column|Data Type|
|---|---|---|
|1| cell_id |Integer|

#### cell_annotation
|No|Column|Data Type|
|---|---|---|
|1| cell_id |Integer|
|2| cell | String |

#### village
|No|Column|Data Type|
|---|---|---|
|1| vill_id |Integer|

#### village_annotation
|No|Column|Data Type|
|---|---|---|
|1| vill_id |Integer|
|2| village | String |


---
`Copyright © 2020 Water and Sanitation Corporation, Ltd., RWANDA`
