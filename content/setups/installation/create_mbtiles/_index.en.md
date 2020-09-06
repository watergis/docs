---
title: Create mbtiles from PostGIS
weight: 22
---

## Create mbtiles from PostGIS (work on `vt`)
- [watergis/postgis2mbtiles](https://github.com/watergis/postgis2mbtiles) : This module will create `mbtiles` by GeoJSON data which is retrieved from `PostGIS`. this module is using [mapbox/tippecanoe](https://github.com/mapbox/tippecanoe), so please use Docker to generate mbtiles if your machine is `Windows`. But you can use the module directly in `MacOS` or `Ubuntu` machine. [watergis/postgis2mbtiles-docker](https://github.com/watergis/postgis2mbtiles-docker) is the source code for Docker implementation. 

First of all, you need to make SQL queries for each layer on `config.js`, so `postgis2mbtiles` tool will extract required data from PostGIS and a mbtiles will be created.

### Basic settings for a layer
The below is a typical example to extract GeoJSON from PostGIS.

```js
{
    name: 'pipeline', //specify your layer name
    geojsonFileName: __dirname + '/pipeline.geojson', //specify geojson name for temporary use
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

There is a special configuration for `tippecanoe` to set minimum zoom level and maximum zoom level.

```sql
row_to_json((
  SELECT t FROM (
    SELECT
      14 as maxzoom,
      11 as minzoom
  ) AS t
)) AS tippecanoe,
```

If your coordinates is not `EPSG:4326`(WGS84), you must transform your coordinate reference system by below SQL.

```sql
ST_TRANSFORM(geom,4326)
```

## Usecases
Making your own SQLs for your database, this step is quite significant. However, it might have some difficulties to create SQLs. For your reference, you can have a look of following two water supply providers' setting.

- `Narok Water and Sewerage Services Co., Ltd, KENYA` : [config.js](https://github.com/narwassco/vt/blob/master/config.js)
- `Water and Sanitation Corporation, Ltd, RWANDA` : [config.js](https://github.com/WASAC/vt/blob/master/config.js)
- `Nakuru Water and Sanitation Services Co., Ltd, KENYA` : [config.js](https://github.com/nakuruwater/vt/blob/master/config.js)

Because this approach can use SQL language to directly extract the data from PostGIS, it can be very frexiblely to adopt any water services providers' GIS database.

### Examples of Vectortiles Design

The design of vectortiles depends on your GIS database and your needs. The below designs are just an example of vectortiles implementation for your reference.

- [Vectortiles Design for Narok water, Kenya](../../../casestudies/narok)
- [Vectortiles Design for WASAC, Rwanda](../../../casestudies/wasac)
