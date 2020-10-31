---
title: Q&A
disableToc: true
---

#### 1. How to change the size of pipe?
This approach can't allow you to edit any data through vector tiles. Vector tiles is static data, that is why it can provide you smooth access to map data. So you have to update the attributes of data from Desktop GIS software such as QGIS or ArcGIS.

---
#### 2. How vector tiles can reduce NRW?
Actually, there is still no good experience for reducing NRW. However, if we can share the GIS data widely with all of colleagues, I think it will help water utility manage NRW more efficient. 

By the way, I am also trying to add new function to integrate EPANET on this WebGIS application. If you can see the result of EPANET simulation, it will be so helpful.

---
#### 3. I'm not sure that I understood well about vector tiles. To create vector tile data, the source data on pipelines should be existed in some database form?
Yes, your GIS data must be stored in certain GIS database. It creates vector tiles tilesets directly from GIS database. This approach uses PostgreSQL/PostGIS because its database is open source. However, you can modify the source code for other database if you are using SQL Server, Oracle and others.

---
#### 4. Does it work offline? Can people view it once they download in the mobile phone or PC? (Like maps.me)
Unfortunately, this is online web application, so you can't see offline. However, you can download mbtiles tilesets to your Android devices, so offline viewing can be available by using QField or INPUT app.

---
#### 5. How can this vector tiles be used in case of water distribution network development projects? 
In Rwanda, we includes some statistics information in vector tiles. So, all of staffs can see any required information for planning water facilities. It can be used for future developments.

---
#### 6. What is the main advantage of Vector Tile over QGIS?
Most of water utilities' GIS administrator actually asked me about editing funcitons. However, WebGIS includes editing is normally extremely expensive. This approach delegated all of editing functions to QGIS side. So, the graphical user interface become very simple and easy to use by other people. You can save a lot of development and training costs.

---
#### 7. To open the data to everybody have some troubles in praivacy. How do you solve this problem?
That is true, if you open some data to public, it will be dangerous sometimes. So you must consider which types of data can be published as open data. In Rwanda's case, we deleted all of privacy information such as client name. In Narok water's case, we deleted searching funciton by client name because of security issue. When you design your own vector tiles, first you should discuss which types of data you can publish.

---
#### 8. Is google maps used as the base map?
No, you can't use Google Maps as base map. Because Google Maps has very restricted license and normally very expensive to use. However, we can use open street map based map which are provided by Mapbox, MapTiler or United Nation Vector Tiles. Also, you can overlay your own base map data on OSM. For instance, in Rwanda and Kenya, we added parcels data of Land Authority on OSM map. It will help most of water utilities especially when they connect new houlsehold meters.