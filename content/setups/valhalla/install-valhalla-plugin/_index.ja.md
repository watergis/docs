---
title: Valhallaプラグインのインストール
weight: 43
---

これでvalhallaサーバーの準備が整いました。このセクションでは、[mapbox-gl-valhalla](https://github.com/watergis/mapbox-gl-valhalla)プラグインをマップに追加していきます。これで valhalla Isochrone API を簡単に使用できるようになります。

- インストール
```bash
npm i @watergis/mapbox-gl-valhalla --save
```

- 使い方

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

- 等時線マップ
![image](https://user-images.githubusercontent.com/2639701/115983404-d7b02c00-a5db-11eb-8328-49ea2ecdd7b8.png)

- 等距離線マップ
![image](https://user-images.githubusercontent.com/2639701/115983424-f0b8dd00-a5db-11eb-9eb8-0e04acaa294e.png)

これで、Mapbox GLアプリケーションにIsochrone機能が追加されました。