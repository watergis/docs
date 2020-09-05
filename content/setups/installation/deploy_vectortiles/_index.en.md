---
title: Deploy vectortiles to gh-pages
weight: 24
---

## Deploy Vector Tile to gh-pages (work on `vt`)

Once your stylefiles' design and mbtiles are completed, now you are ready to deploy your vector tiles to gh-pages. [postgis2vectortiles](https://github.com/watergis/postgis2vectortiles) will assist you to create and deploy vector tiles.

There are two cases for deploying.

{{<mermaid align="center">}}
graph LR
	A[mbtiles] --> B{Is your coverage area large?}
  B -->|No|C[narwassco/vt-map]
	B -->|Yes|D[wasac/vt]
  C -->|produce tiles locally|E[gh-pages]
  D -->|upload mbtiles|F[github master branch]
  F -->|produce tiles by Github Actions|E
{{< /mermaid >}}

### i. [narwassco/vt-map approach] A case of Narok Water, Kenya
If your coverage area is small, you can use the approach of `Narok Water` to deploy. Please have a look following repository.

- [narwassco/vt-map](https://github.com/narwassco/vt-map)
  This module will use the following submodules to create Mapbox Vector Tile for deployment to gh-pages.
  - [watergis/postgis2mbtiles](https://github.com/watergis/postgis2mbtiles): It creates `mbtiles` from PostGIS.
  - [watergis/mbtiles2pbf](https://github.com/watergis/mbtiles2pbf): It converts from `mbtiles` to `pbf(mvt)` tiles.

This module uses [mapbox/tippecanoe](https://github.com/mapbox/tippecanoe) for producing mbtiles and uses [mbutil](https://github.com/mapbox/mbutil) to convert `mbtiles`. However, Narok water's GIS computer is Windows 10 Pro, so it is not easy to run `tippecanoe`, I developed `Docker` to create Mapbox Vector Tile.

### ii. [WASAC/vt approach] A case of WASAC, Rwanda (Recommended)
If your coverage area is huge, I am afraid it is not easy to deploy thousands of vector tiles to Github pages. So you can use `WASAC` approach to deploy `mbtiles` first, then use `Github Actions` to extract vector tiles from your `mbtiles`. You can see the following repository for your reference.

- [WASAC/vt](https://github.com/WASAC/vt)
  This module will use the following submodules to create Mapbox Vector Tile for deployment to gh-pages.
  - [watergis/postgis2mbtiles](https://github.com/watergis/postgis2mbtiles): It creates `mbtiles` from PostGIS. `postgis2mbtiles` module will run on your local computer.
  - [watergis/mbtiles2pbf](https://github.com/watergis/mbtiles2pbf): It converts from `mbtiles` to `pbf(mvt)` tiles. `mbtiles2pbf` will run on `Github Actions`.

The below is a workflow file of `Narok Water` to automate deploy pbf files from mbtiles by `Github Actions`.

```yaml
name: Node.js CI

on:
  push:
    branches: [ master ]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2
    - name: Use Node.js
      uses: actions/setup-node@v1
      with:
        node-version: 12.x
    - run: npm ci
      env:
        NODE_AUTH_TOKEN: ${{secrets.GITHUB_TOKEN}}
    - run: npm run extract
    - name: configure git and deploy
      env:
        NODE_AUTH_TOKEN: ${{secrets.GITHUB_TOKEN}}
      run: |
        git config --global user.name "narwassco+githubci"
        git config --global user.email "narwassco+githubci@users.noreply.github.com"
        git remote set-url origin https://x-access-token:${NODE_AUTH_TOKEN}@github.com/narwassco/vt.git
        npm run deploy
```

- `Narok Water` also started using [`WASAC/vt` approach] instead [`narwassco/vt-map` approach]. 
  - [narwassco/vt](https://github.com/narwassco/vt)

- `Nakuru Water` also started using [`WASAC/vt` approach]. 
  - [nakuruwater/vt](https://github.com/nakuruwater/vt)