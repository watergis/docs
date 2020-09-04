---
title: Credits
disableToc: true
---

## Contributors

Thanks to them for making Open Source Software a better place !

And a special thanks to the below contributors.
- [@JinIgarashi](https://github.com/JinIgarashi) for his work on [watergis](https://github.com/watergis)
- [United Nation Open GIS Initiative](http://unopengis.org/)'s [UN Vector Tile Toolkit](https://github.com/unvt) to support us technically.

## Packages and libraries
All of libraries are under **MIT** license.

### 1. Software for Mapbox GL JS client
- [watergis/mapbox-gl-legend](https://github.com/watergis/mapbox-gl-legend): Add a simple legend control
- [watergis/mapbox-gl-area-switcher](https://github.com/watergis/mapbox-gl-area-switcher): Add a simple control to switch area easier
- [watergis/mapbox-gl-popup](https://github.com/watergis/mapbox-gl-popup): add a simple popup into Mapbox GL JS.
- [watergis/mapbox-gl-print](https://github.com/watergis/mapbox-gl-print): add a simple print control to export PNG and PDF.
- [watergis/mapbox-gl-pitch-toggle-control](https://github.com/watergis/mapbox-gl-pitch-toggle-control): add a simple 3D button to change between 3D and 2D

### 2. Software for Vectortiles
- [watergis/vt-boilerplate](https://github.com/watergis/vt-boilerplate): a template to create vectortiles from PostGIS and deploy it to Github pages.
- [watergis/postgis2geojson](https://github.com/watergis/postgis2geojson): a module to extract GeoJSON directly from PostGIS.
- [watergis/postgis2mbtiles](https://github.com/watergis/postgis2mbtiles): a module to extract mbtiles directly from PostGIS.
- [watergis/postgis2mbtiles-docker](https://github.com/watergis/postgis2mbtiles-docker): a Docker implementation for `postgis2mbtiles` module.
- [watergis/mbtiles2pbf](https://github.com/watergis/mbtiles2pbf): a module to convert from mbtiles to pbf(mvt) vectortiles.
- [watergis/postgis2vectortiles](https://github.com/watergis/postgis2vectortiles): a module to create pbf vectortiles from PostGIS directly.
- [watergis/sprite-creator](https://github.com/watergis/sprite-creator): a module to create sprite files from SVG icons.

### 3. Software for EPANET
- [watergis/geojson2inp](https://github.com/watergis/geojson2inp): a module create INP file from GeoJSON files.
- [watergis/postgis2inp](https://github.com/watergis/postgis2inp): a module create INP file directly from PostGIS.

## Vectortiles Implementation
Actual vectortiles datas are owned by their water companies. Vectortiles data are located in following repositories.

- [narwassco/vt](https://github.com/narwassco/vt): Vectortiles for Narok Water, Kenya
- [WASAC/vt](https://github.com/WASAC/vt): Vectortiles for WASAC, Rwanda
- [nakuruwater/vt](https://github.com/nakuruwater/vt): Vectortiles for Nakuru Water, Kenya

Thanks all of officers in the above water services providers to collect and maintain the GIS data.

### License of vectortiles data
Those vectortiles are licensed under a [Creative Commons Attribution 4.0 International
License](http://creativecommons.org/licenses/by/4.0/).

If you want to use their open data, please mention their attiribution. For instance,

- Attribution of Narok Water, Kenya
```
Copyright (c) 2020 Narok Water and Serwerage Services Co, Ltd.
```
- Atribution of WASAC, Rwanda
```
Copyright (c) 2020 Water and Sanitation Corporation, Ltd.
```
- Attribution of Nakuru Water, Kenya
```
Copyright (c) 2020 Nakuru Water and Sanitation Services Co, Ltd.
```

Also, if you want to use our stylefiles together with base map, please put the following additional attribution on your map.

```
(c)Mapbox, (c) OpenStreetMap contributors, Powered by the United Nations Vector Tile Toolkit
```

## Stylefiles and Spritefiles
Those stylefiles and spritefiles are following [Mapbox Style Specification](https://docs.mapbox.com/mapbox-gl-js/style-spec/). The repositories are as follows.

- [narwassco/mapbox-stylefiles](https://github.com/narwassco/mapbox-stylefiles): Stylefiles for Narok Water, Kenya
- [WASAC/mapbox-stylefiles](https://github.com/WASAC/mapbox-stylefiles): Stylefiles for WASAC, Rwanda.
- [nakuruwater/mapbox-stylefiles](https://github.com/nakuruwater/mapbox-stylefiles): Stylefiles for Nakuru Water, Kenya

Those stylefiles are licenced under `C0-1.0 License`. However, we are using some icons of Mapbox Studio. So those icons which are from Mapbox, the license also belong them.
