---
title: Deploy Mapbox Stylefiles and Sprite files to gh-pages
weight: 25
---

## Deploy Mapbox Stylefiles and Sprite files on gh-pages
- [watergis/sprite-creater](https://github.com/watergis/sprite-creator) : This module will assist you to create sprite files from your icons. 

- Please create a repository which can be named `mapbox-stylefiles`. You can organize stylefiles and sprite files as following structures.

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

### Use cases
There are the following use cases. You may fork one of the repositories and adopted to your own needs.
- `Narok Water and Sewerage Services Co., Ltd, KENYA` : [narwassco/mapbox-stylefiles](https://github.com/narwassco/mapbox-stylefiles)
- `Water and Sanitation Corporation, Ltd, RWANDA` : [WASAC/mapbox-stylefiles](https://github.com/WASAC/mapbox-stylefiles)
- `Nakuru Water and Sanitation Services Co., Ltd, KENYA` : [nakuruwater/mapbox-stylefiles](https://github.com/nakuruwater/mapbox-stylefiles)

## Create sprite files from your icons

The Spritefiles will be generated from [mapbox/maki](https://github.com/mapbox/maki) icons and [water-icons](https://github.com/narwassco/water-icons) icons under `docs` of this repository. `UNVT` basemap is using `mapbox/maki` icons. In `Narok Water`'s case, the following repositories manage our icons which are being used in our style files.
  - [narwassco/water-icons](https://github.com/narwassco/water-icons) : It includes our own customized icon for water assets.
  - [narwassco/mapbox-street-icons](https://github.com/narwassco/mapbox-street-icons) : It includes icons of Mapbox Street style.
  - [narwassco/mapbox-satellite-icons](https://github.com/narwassco/mapbox-satellite-icons):It includes icons of Mapbox Satellite style.

## Put your Mapbox Stylefiles

You can download your Mapbox Stylefiles from Mapbox Studio, then you can delete unnecessary contents from the stylefile, and changed url of `vector tile` and `sprite file` on it. 

Particulally, you must change `sources`, `sprite` and `glyphs` properties as follows.
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

Then, you are going to `layers` properties to change `source` name.
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