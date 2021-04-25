---
title: Install Valhalla Plugin
weight: 43
---

Now, your valhalla server is ready. In this section, we are going to add [mapbox-gl-valhalla](https://github.com/watergis/mapbox-gl-valhalla) plugin into your map. So you can use valhalla Isochrone API easily.

- Installation
```bash
npm i @watergis/mapbox-gl-valhalla --save
```

- Usage

```js
import { MapboxValhallaControl} from "@watergis/mapbox-gl-valhalla";
import '@watergis/mapbox-gl-valhalla/css/styles.css';
import mapboxgl from 'mapbox-gl';

const map = new mapboxgl.Map();
map.addControl(new MapboxValhallaControl(
  'http://localhost:8002',
  {
    Contours: [
      {
        time: 3,
        distance: 1,
        color: 'ff0000',
      },
      {
        time: 5,
        distance: 2,
        color: 'ffff00',
      },
      {
        time: 10,
        distance: 3,
        color: '0000ff',
      },
    ]
  }
), 'top-right');
```

- Time Isochrone Map
![image](https://user-images.githubusercontent.com/2639701/115983404-d7b02c00-a5db-11eb-8328-49ea2ecdd7b8.png)

- Distance Isochrone Map
![image](https://user-images.githubusercontent.com/2639701/115983424-f0b8dd00-a5db-11eb-9eb8-0e04acaa294e.png)

Now, Isochrone function was added into your Mapbox GL application!