---
title: Installation
weight: 20
---

In this section, we will show you how to generate vector tiles.

First of all, you can understand our toolkit's whole procedures in the below image.

## System Diagram
![vectortiles-system-structure](./vectortiles-system-structure.png?width=50pc)

## Sequence Diagram of vectortiles production in the toolkits

{{<mermaid align="center">}}
sequenceDiagram
    participant db as PostGIS
    participant x as User
    participant a as postgis2mbtiles
    participant b as postgis2vectortiles
    participant d as mapbox-stylefiles
    participant y as Mapbox Studio
    participant z as gh-pages

    db->>a: GeoJSON
    Note over a: tippecanoe
    a->>x: mbtiles
    
    x->>y: Upload mbtiles
    y->>y: Edit Mapbox Stylefiles
    Note over y: Stylefile editing

    x->>x: configure settings for postgis2vectortiles
    db->>b: GeoJSON
    b->>z: Mapbox Vectortiles (pbf tile) 
    Note over b: Upload to gh-pages

    y->>x: Download Mapbox Stylefiles and SVG icons
    x->>x: Edit Stylefiles for gh-pages
    x->>d: produce Stylefiles
    x->>d: produce sprite files
    d->>z: Mapbox Stylefiles and Sprite files

    x-->>x: Develop Web app by Mapbox GL JS
    x->>z: Upload HTML/JavaScript
{{< /mermaid >}}

## Next

Now, we are going to see detailly how to implement your own vectortiles.