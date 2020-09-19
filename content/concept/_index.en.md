---
title: Concept
weight: 1
pre: "<b>1. </b>"
chapter: true
---

### Chapter 1

#### 1. Concept
- To enable small organizations like water services provider to share and utilize their GIS data easily.
- To make operation & maintenance of vector tiles at the lowest cost as much as possible.

#### 2. Why did I develop this tool?
After collecting GIS data of water, most water services providers in Africa often failed to share and utilize the data because of limited budget and know-how. As a result, the GIS data will not be up-to-date at all. They will need to collect the same GIS data again after several years. It is not efficient actually.

I have been looking for a way to keep their motivation to maintain the data continuously by having the water GIS data widely used through WebGIS. Recently, I became involved in a technology called **vector tiles**, then I developed this open source tool for water services providers.

#### 3. Objectives
- To establish the effective way to share and utilize GIS data with all staffs after data collection
- To utilize GIS data more in order to make waterworks efficiency
- To use GIS data for all type of waterworks in utility (NOT ONLY for NRW and water distribution)

#### 4. Current situation for utilizing GIS in water services providers
GIS is very useful tool in order to make daily waterworks effective, and nowadays most of water utilities started to use GIS.

However, there are some challenges usually:
- Very limited access to GIS data
- Requires high level skill of GIS for utilizing, it is quite difficult to use.
- It costs too much to procure GIS software and provide trainings
- Poor internet connection interrupt to share data via internet

In order to solve such as above situation, I recommend that you introduce vector tiles that can operate GIS data more sustainably and at low cost as open source and open data.

#### 5. Utilize Open Source & Open Data
If we use open source software and make the data be at public domain, operational costs will be free of charge up to a certain usage. This makes it a good option for small oranizations which want to operate at a low cost.

- To use **FOSS4G** (Free & Open Source Software for Geospatial) software such as QGIS, PostGIS.
  - Significantly lower cost than proprietary products such as ArcGIS
- Implement serverless by using **Gihub Pages**
  - Easy to implement because no GIS server is needed
- To use **WebGIS** which has user friendly interface like Google Map
  - WebGIS does not need the advanced skills which is required for ArcGIS and QGIS.
  - Minimize the cost of training by using WebGIS
- To use **vector tiles** for data distribution
  - It is significantly lighter and less expensive to generate vector tiles than raster tiles such as WMS and TMS.
  - More stable and faster than dynamic vector data distribution such as WFS.

#### 6. Possibilities to utilize vector tiles in water services providers
For instance, the following are possible uses:
- It can be effectively used as a measure against **Non-Revenue Water (NRW)**.
- **Plumbers** can easily access vect tiles before constructing their waterworks to get a more efficient view of what's going on in the field.
- **Meter readers** can use vector tiles in the field to more efficiently read meters.
- **Customer care** can use vector tiles when dealing with clients. It can lead to more appropriate responses and customer satisfaction.
- **Manager** can use vector tiles effectively for future planning of water networks, as well as for briefing and sharing with stakeholders like the Government and financial institubion.
- By making it **open data**, data can be shared with people outside the water sector. There are various possibilities and synergistic effects in the future, such as collaboration with private companies.

However, there are few examples of water supply data being used as open data at the moment. Therefore, how to utilize water supply vector tiles needs to be explored through trial and error. 

How you utilize it is completely up to your organization!