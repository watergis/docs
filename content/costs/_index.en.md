---
title: Costs of O&M
weight: 15
pre: "<b>3. </b>"
chapter: true
---

### Chapter 3

This chapter will show you how to generate vector tiles

This system is fully adopted to GitHub Pages platform. 

This application can work without server, and Github provides HTTPS secure connection as default. Basically, it costs completely free of charge, you don't need additional fees for operating vectortiles services.

However, there are some limits in GitHub Pages and BaseMap services as follows.

## 1. Hosting Service of GitHub Pages
Although GitHub Pages is free of charges for an Open Source Project, there are some usage limits. See more details about GitHub Pages [here](https://docs.github.com/en/github/working-with-github-pages/about-github-pages).
* GitHub Pages source repositories have a recommended limit of 1GB.
* Published GitHub Pages sites may be no larger than 1 GB.
* GitHub Pages sites have a soft bandwidth limit of 100GB per month.
* GitHub Pages sites have a soft limit of 10 builds per hour.

### In case of WASAC, Rwanda
WASAC's Vectortiles data in the whole country is currently only approximately 33MB. So I think our usage should not be a problem.

### In case of Narok Water, Kenya
Narok Water's Vectortiles data is currently only approximately 2MB. So I think our usage should not be a problem.

## 2. Usage of Base map from Mapbox Studio
Our vectortiles client application [mapbox-gl-js-client](https://github.com/narwassco/mapbox-gl-js-client) is using base map services of [Mapbox Studio](https://www.mapbox.com). Mapbox Studio can provides very beautiful vectortile based OpenStreetMap.

Currently, we are using free plan of Mapbox Studio. However, there are also some limits.
* Map Loads for Web : 50,000 request per month

If requests exceed 50,000, they will charge $5 USD per 1000 request.
You can see more details about their pricing [here](https://www.mapbox.com/pricing/).

### Cost Estimation in case of WASAC, Rwanda
I estimated the number of page views is approximately `41,400` per month. I estimated 30 days per month because some waterworks need to be done during weekends. However, I don't think all of people will access fully. So, 50,000 requests' limit is still enough.

If WASAC's usage will exceed 50,000 requests, we may consider to change base map services from Mapbox to Maptiler. Maptiler will provide base map for free of charge upto 100,000 requests per month. You can see more details about Maptiler's pricing [here](https://www.maptiler.com/cloud/plans/). 

| Organization | No of Organization | No of Users per Organizaiton | Total No of Users | Page Views per person per day | Total PVs per day | Estimated PV per month |
|-|-|-|-|-|-|-|
| Districts | 30 | 1 | 30 | 3 | 90 | 2700 |
| POs | 80 | 5 | 400 | 3 | 1200 | 36000 |
| WASAC RWSS | 1 | 30 | 30 | 3 | 90 | 2700 |
| Total | 111 | 36 | 460 | - | 1380 | **41400** |

### Cost Estimation in case of Narok Water, Kenya
I estimated the number of page views is approximately `10500` per month. Its capacity is much enough to use within `50,000` page views per month.

| Organization | No of Organization | No of Users per Organizaiton | Total No of Users | Page Views per person per day | Total PVs per day | Estimated PV per month |
|-|-|-|-|-|-|-|
| NARWASSCO | 1 | 70 | 70 | 5 | 350 | **10500** |
