---
title: Requirements
weight: 5
pre: "<b>1. </b>"
chapter: true
---

### Chapter 1

What is required for developing vectortiles in a water services providers?

## 1. Install PostgresSQL/PostGIS database

This vectortiles toolkit uses PostgreSQL/PostGIS database. So, please try to install it in your computer.

- [PostgreSQL](https://www.postgresql.org)
- [PostGIS](https://postgis.net)

If you will install new one, I think you can install PostgreSQL12 and PostGIS3.1. I recommend to use at least more than PostgreSQL11 and PostGIS2.5.

## 2. Data Collection and Import data into PostGIS database

If you don't have any GIS data yet, you must go to data collection first. You might need some GPS devices such as `Trimble` or `Garmin`. But you can also use following smartphone applications for data collection.

- [QField for QGIS](https://qfield.org): It works on Android.
- [Input](https://inputapp.io/en/): It works on both iOS and Android.

Both applications are free and open source, it is completely compatible to QGIS. However, I personally recomment to use QField which is more advanced and user friendly.

If you need some assists about data collection, please let me know.

## 3. Install Docker

This toolkit uses `Docker` to generate vectortiles from PostGIS database in order to use `tippecanoe` tool. So, please install `Docker` in your computer.

### Docker Desktop on Windows
See [official webpage](https://docs.docker.com/docker-for-windows/install/) to install it.

- Please make sure you selected `Linux container`(`Windows container` is incorrect!)
- Please enable your Hyper-V in your computer.

### Docker Desktop on MacOS
See [official webpage](https://docs.docker.com/docker-for-mac/) to install it by `Homebrew`.

```bash
brew search docker
brew cask install docker
```

### Docker on Ubuntu
See [official webpage](https://docs.docker.com/engine/install/ubuntu/) to install it

## To Next
That's all!! Now you are ready to implement your vectortiles!
