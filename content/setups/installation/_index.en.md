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
    participant user as User
    participant vt as vt
    participant style as mapbox-stylefiles
    participant mapbox as Mapbox Studio
    participant action as Github Actions
    participant ghpages as gh-pages

    db->>vt: GeoJSON
    Note over vt: tippecanoe
    vt->>user: mbtiles
    
    user->>mapbox: Upload mbtiles
    mapbox->>mapbox: Edit Mapbox Stylefiles
    Note over mapbox: Stylefile editing

    db->>vt: GeoJSON
    Note over vt: Once stylefile is ready
    vt->>action: Upload mbtiles
    action->>ghpages: Vector tiles(pbf/mvt) 
    Note over action: Build & Deploy

    mapbox->>user: Download Mapbox Stylefiles and SVG icons
    user->>user: Edit Stylefiles for gh-pages
    user->>style: generate Stylefiles
    user->>style: generate sprite files
    style->>ghpages: Deploy Style files and Sprite files

    user-->>user: Develop Web app by Mapbox GL JS
    user->>action: Upload HTML/JavaScript
    action->>ghpages: HTML/JavaScript
    Note over action: Build & Deploy
{{< /mermaid >}}

## Next

Now, we are going to see detailly how to implement your own vectortiles.