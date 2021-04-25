---
title: Packages and libraries
weight: 50
pre: "<b>5. </b>"
chapter: true
---

### Chapter 5

This chapter will show you the list of our open source projects.

All of libraries are in [Github](https://github.com/watergis) under **MIT** license.

#### 1. Software for Mapbox GL JS client
- [watergis/mapboxgljs-boilerplate](https://github.com/watergis/mapboxgljs-boilerplate): This is the template of Mapbox GL JS implementation for Water Services Providers with all of customized plugins.
- [watergis/mapbox-gl-legend](https://github.com/watergis/mapbox-gl-legend): Add a simple control that can generate a legend from map style
- [watergis/mapbox-gl-area-switcher](https://github.com/watergis/mapbox-gl-area-switcher): Add a simple control to switch area easier
- [watergis/mapbox-gl-popup](https://github.com/watergis/mapbox-gl-popup): add a simple popup into Mapbox GL JS.
- [watergis/mapbox-gl-export](https://github.com/watergis/mapbox-gl-export): add a simple control that exports a map as PNG or PDF.
- [watergis/mapbox-gl-pitch-toggle-control](https://github.com/watergis/mapbox-gl-pitch-toggle-control): add a simple 3D button to change between 3D and 2D
- [watergis/mapbox-gl-elevation](https://github.com/watergis/mapbox-gl-elevation): adds elevation control to mapbox-gl. It relys on terrain RGB raster tilesets.
- [watergis/mapbox-gl-valhalla](https://github.com/watergis/mapbox-gl-valhalla): adds a control which can integrate with valhalla api.

#### 2. Software for Vectortiles
- [watergis/vt-boilerplate](https://github.com/watergis/vt-boilerplate): a template to create vectortiles from PostGIS and deploy it to Github pages.
- [watergis/postgis2geojson](https://github.com/watergis/postgis2geojson): a module to extract GeoJSON directly from PostGIS.
- [watergis/postgis2mbtiles](https://github.com/watergis/postgis2mbtiles): a module to extract mbtiles directly from PostGIS.
- [watergis/postgis2mbtiles-docker](https://github.com/watergis/postgis2mbtiles-docker): a Docker implementation for `postgis2mbtiles` module.
- [watergis/mbtiles2pbf](https://github.com/watergis/mbtiles2pbf): a module to convert from mbtiles to pbf(mvt) vectortiles.
- [watergis/postgis2vectortiles](https://github.com/watergis/postgis2vectortiles): a module to create pbf vectortiles from PostGIS directly.
- [watergis/sprite-creator](https://github.com/watergis/sprite-creator): a module to create sprite files from SVG icons.
- [watergis/mvt-generator](https://github.com/watergis/mvt-generator): This module creates MVT tiles directly from PostGIS

#### 3. Software for EPANET
- [watergis/geojson2inp](https://github.com/watergis/geojson2inp): a module create INP file from GeoJSON files.
- [watergis/postgis2inp](https://github.com/watergis/postgis2inp): a module create INP file directly from PostGIS.

#### 4. Software for Elevation
- [watergis/dem2terrainrgb](https://github.com/watergis/dem2terrainrgb): a python module to convert DEM to terrain RGB raster tiles.
- [watergis/terrain-rgb](https://github.com/watergis/terrain-rgb): a typescript module to extract elevation from terrain RGB tilesets by longitude and latitude.

#### 5. Software for Elasticsearch
- [watergis/es_tileserv](https://github.com/watergis/es_tileserv): a simple vector tile server which is served from Elasticsearch.
- [watergis/elastic2mvt](https://github.com/watergis/elastic2mvt):  a Nodejs module that generate Mapbox vector tiles from Elasticsearch.