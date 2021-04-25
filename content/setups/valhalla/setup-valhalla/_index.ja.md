---
title: Valhallaのセットアップ
weight: 41
---

## GCPにインスタンスを作成する

テストのためにGCPの無料利用枠を利用することができます。アメリカリージョンの`f1.micro`インスタンスは、永久に無料で使うことができます。

しかし、`f1.micro` で Valhalla をコンパイルしようとすると、うまく動作しません。Valhalla をコンパイルする際には、インスタンスタイプをアップグレードする必要があるかもしれません。少なくとも、`e2.smal`であれば、うまく動作させることができるでしょう。


## 事前準備

```bash
$ sudo add-apt-repository -y ppa:valhalla-core/valhalla
$ sudo apt-get update
$ sudo apt-get install -y cmake make libtool pkg-config g++ gcc curl unzip jq lcov protobuf-compiler vim-common locales libboost-all-dev libcurl4-openssl-dev zlib1g-dev $ liblz4-dev libprime-server-dev libprotobuf-dev prime-server-bin parallel
#if you plan to compile with data building support, see below for more info
$ sudo apt-get install -y libgeos-dev libgeos++-dev libluajit-5.1-dev libspatialite-dev libsqlite3-dev wget sqlite3 spatialite-bin
$ source /etc/lsb-release
$ if [[ $(python -c "print(int($DISTRIB_RELEASE > 15))") > 0 ]]; then sudo apt-get install -y libsqlite3-mod-spatialite; fi
#if you plan to compile with python bindings, see below for more info
$ sudo apt-get install -y python-all-dev

$ sudo ln -s /usr/bin/python3 /usr/bin/python
# add following 2 lines into the file.
$ vi ~/.bash_aliases
alias python="python3" 
alias pip="pip3" 
```

## インストールとコンパイル

この処理には少し時間がかかるかもしれません...

```bash
$ git clone --recurse-submodules https://github.com/valhalla/valhalla.git
$ mkdir build
$ cd build
$ cmake .. -DCMAKE_BUILD_TYPE=Release
$ make -j$(nproc) # for macos, use: make -j$(sysctl -n hw.physicalcpu)
$ sudo make install
```

## タイルの生成

ここではルワンダのタイルを生成していきます。

```bash
# osm.pbfのダウンロード
$ wget http://download.geofabrik.de/africa/rwanda-latest.osm.pbf

# フォルダの作成
$ mkdir -p valhalla_tiles
$ mkdir -p elevation_tiles

# 標高タイルの作成
$ valhalla_build_elevation 28.776751931346325 30.973689303919286 -2.9252966743046187 -1.0090709211361428 ./elevation_tiles $(nproc)

# 設定ファイルの作成
$ valhalla_build_config --mjolnir-tile-dir ${PWD}/valhalla_tiles --mjolnir-tile-extract ${PWD}/valhalla_tiles.tar --mjolnir-timezone ${PWD}/valhalla_tiles/timezones.sqlite --mjolnir-admin ${PWD}/valhalla_tiles/admins.sqlite --additional-data-elevation ${PWD}/elevation_tiles > valhalla.json

# Adminファイルの作成
$ valhalla_build_admins --config valhalla.json rwanda-latest.osm.pbf

# Valhallaタイルの作成
$ valhalla_build_tiles -c valhalla.json rwanda-latest.osm.pbf

# タイルができているか確認
$ find valhalla_tiles | sort -n | tar cf valhalla_tiles.tar --no-recursion -T -

# サーバーの起動
$ valhalla_service valhalla.json 1

# 下のURLでチェックしてみる
curl --globoff http://localhost:8002/isochrone?json={"locations":[{"lat":-1.946357,"lon":30.059753}],"costing":"pedestrian","contours":[{"time":15,"color":"ff0000"},{"time":30,"color":"ffff00"},{"time":60,"color":"0000ff"}]} | jq '.'

# ctrl + cを押してサーバーを停止
```

[こちら](https://valhalla.readthedocs.io/en/latest/api/isochrone/api-reference/#inputs-of-the-isochrone-service)でIsochrone APIについてのドキュメントを閲覧できます。

インストールの結果は以下のようになるでしょう。

```bash
$ valhalla_build_tiles -c valhalla.json rwanda-latest.osm.pbf kenya-latest.osm.pbf
2021/04/05 23:09:36.448293 [INFO] Start stage = initialize End stage = cleanup
2021/04/05 23:09:36.481539 [WARN] Non-empty /home/jin_igarashi/valhalla_tiles/0 will be purged of tiles
2021/04/05 23:09:36.497076 [WARN] Non-empty /home/jin_igarashi/valhalla_tiles/1 will be purged of tiles
2021/04/05 23:09:36.500313 [WARN] Non-empty /home/jin_igarashi/valhalla_tiles/2 will be purged of tiles
2021/04/05 23:09:36.540027 [INFO] Parsing files for ways: rwanda-latest.osm.pbf, kenya-latest.osm.pbf
2021/04/05 23:09:36.541720 [INFO] Parsing ways...
2021/04/05 23:10:09.405681 [INFO] Finished with 641611 routable ways containing 14714643 nodes
2021/04/05 23:10:09.820947 [INFO] Sorting osm access tags by way id...
2021/04/05 23:10:09.822863 [INFO] Finished
2021/04/05 23:10:09.867780 [INFO] Parsing files for relations: rwanda-latest.osm.pbf, kenya-latest.osm.pbf
2021/04/05 23:10:09.882279 [INFO] Parsing relations...
2021/04/05 23:10:37.054207 [INFO] Finished with 72 simple restrictions
2021/04/05 23:10:37.054446 [INFO] Finished with 0 lane connections
2021/04/05 23:10:37.134344 [INFO] Sorting complex restrictions by from id...
2021/04/05 23:10:37.135849 [INFO] Sorting complex restrictions by to id...
2021/04/05 23:10:37.136018 [INFO] Finished
2021/04/05 23:10:37.138039 [INFO] Parsing files for nodes: rwanda-latest.osm.pbf, kenya-latest.osm.pbf
2021/04/05 23:10:37.138158 [INFO] Sorting osm way node references by node id...
2021/04/05 23:12:11.570500 [INFO] Parsing nodes...
2021/04/05 23:13:51.381136 [INFO] Finished with 13786564 nodes contained in routable ways
2021/04/05 23:13:51.381545 [INFO] Sorting osm way node references by way index and node shape index...
2021/04/05 23:15:42.570426 [INFO] Finished: max_osm_id 8593165265
2021/04/05 23:15:42.570850 [INFO] Number of nodes with refs (exits) = 40
2021/04/05 23:15:42.570861 [INFO] Number of nodes with exit_to = 1
2021/04/05 23:15:42.570868 [INFO] Number of nodes with names = 85
2021/04/05 23:15:42.570901 [INFO] Number of way refs = 0
2021/04/05 23:15:42.570909 [INFO] Number of reverse way refs = 0
2021/04/05 23:15:42.570917 [INFO] Unique Node Strings (names, refs, etc.) = 96
2021/04/05 23:15:42.570924 [INFO] Unique Strings (names, refs, etc.) = 8411
2021/04/05 23:15:42.631193 [INFO] Creating graph edges from ways...
2021/04/05 23:15:53.262235 [INFO] Finished with 1364899 graph edges
2021/04/05 23:15:53.701871 [INFO] Sorting graph...
2021/04/05 23:16:03.332275 [INFO] Nodes processed. Sorting begin and end nodes by edge.
2021/04/05 23:16:04.910107 [INFO] Sorting begin and end nodes done. Populating edges...
2021/04/05 23:16:05.626580 [INFO] Finished with 1078431 graph nodes
2021/04/05 23:16:05.783283 [INFO] Writing tile manifest to /home/jin_igarashi/valhalla_tiles/tile_manifest.json
2021/04/05 23:16:05.841529 [INFO] Reclassifying link graph edges...
2021/04/05 23:16:06.609826 [INFO] Class: 0 exit count = 0
2021/04/05 23:16:06.610659 [INFO] Class: 1 exit count = 403
2021/04/05 23:16:06.610705 [INFO] Class: 2 exit count = 147
2021/04/05 23:16:06.610738 [INFO] Class: 3 exit count = 366
2021/04/05 23:16:06.610803 [INFO] Class: 4 exit count = 209
2021/04/05 23:16:06.610839 [INFO] Class: 5 exit count = 93
2021/04/05 23:16:06.610870 [INFO] Class: 6 exit count = 111
2021/04/05 23:16:06.610901 [INFO] Class: 7 exit count = 0
2021/04/05 23:16:12.556352 [INFO] Finished with 905 reclassified.  Turn channel count = 636
2021/04/05 23:16:12.596027 [INFO] Reclassifying ferry connection graph edges...
2021/04/05 23:16:32.677942 [INFO] Finished ReclassifyFerryEdges: ferry_endpoint_count = 10, 884 edges reclassified.
2021/04/05 23:16:32.936976 [INFO] Building 877 tiles with 1 threads...
2021/04/05 23:16:32.955428 [WARN] Admin db /home/jin_igarashi/valhalla_tiles/admins.sqlite not found.  Not saving admin information.
2021/04/05 23:16:32.955571 [WARN] Time zone db /home/jin_igarashi/valhalla_tiles/timezones.sqlite not found.  Not saving time zone information.
2021/04/05 23:22:31.510882 [INFO] Finished
2021/04/05 23:22:31.642744 [INFO] Node Count = 1078431
2021/04/05 23:22:31.642899 [INFO] Directed Edge Count = 2729798
2021/04/05 23:22:31.642941 [INFO] EdgeInfo Count = 1381991
2021/04/05 23:22:31.643023 [INFO] Enhancing local graph...
2021/04/05 23:22:31.914998 [WARN] Admin db /home/jin_igarashi/valhalla_tiles/admins.sqlite not found.  Not saving admin information.
2021/04/05 23:25:54.623910 [WARN] Exceeding maximum.  Average speed: 150
2021/04/05 23:25:54.626779 [WARN] Exceeding maximum.  Average speed: 150
2021/04/05 23:30:19.586500 [INFO] Finished with max_density 23.131340
2021/04/05 23:30:19.586855 [INFO] internal intersection = 3021
2021/04/05 23:30:19.604294 [INFO] GraphFilter - nothing to filter. Skipping...
2021/04/05 23:30:19.646568 [INFO] Transit directory not found. Transit will not be added.
2021/04/05 23:30:19.661688 [INFO] HierarchyBuilder
2021/04/05 23:31:17.521323 [INFO] Done HierarchyBuilder
2021/04/05 23:31:17.592629 [INFO] Creating shortcuts on level 1
2021/04/05 23:31:20.267091 [INFO] Finished with 13766 shortcuts
2021/04/05 23:31:20.267264 [INFO] Creating shortcuts on level 0
2021/04/05 23:31:20.925292 [INFO] Finished with 2652 shortcuts
2021/04/05 23:31:20.927401 [INFO] ElevationBuilder: no elevation data, skipping
2021/04/05 23:31:21.173273 [INFO] Adding Restrictions at level 2
Killed
```

## 自動的に起動するようにする

サーバーの起動時に自動的にValhallaを起動するようにします。

- 起動スクリプトの作成
```bash
$ cd ~
$ vi start_valhalla.sh
```

`start_valhalla.sh`は以下のようになるでしょう。
```bash
#!bin/bash
cd /home/jin_igarashi
valhalla_service valhalla.json 1
```

```
$ chmod +x start_valhalla.sh
```

- valhallaサービスの作成

```bash
sudo vi /etc/systemd/system/valhalla.service
```

`valhalla.service`は以下のようになるでしょう。
```bash
[Unit]
Description = valhalla service
After=local-fs.target
ConditionPathExists=/home/jin_igarashi

[Service]
ExecStart=/home/jin_igarashi/start_valhalla.sh
Restart=no
Type=simple


[Install]
WantedBy=multi-user.target
```

```bash
sudo chmod 644 /etc/systemd/system/valhalla.service
sudo systemctl daemon-reload
sudo systemctl status valhalla.service
sudo systemctl enable valhalla.service
sudo systemctl start valhalla.service
```

- ログを見る
```
journalctl -u valhalla.service
```

- サービスの再起動
```
sudo systemctl restart valhalla.service
```

- サービスの停止
```
sudo systemctl stop valhalla.service
```