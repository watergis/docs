---
title: ベクトルタイルのgh-pagesへのデプロイ
weight: 24
---

## ベクトルタイルのgh-pagesへのデプロイ(`vt`で作業)

スタイルファイルのデザインとmbtilesが完成したら、いよいよベクトルタイルをgh-pagesにデプロイします。[postgis2vectortiles](https://github.com/watergis/postgis2vectortiles)のモジュールがベクトルタイルの生成とデプロイを一貫して行なってくれます。

デプロイするには二つのケースがあります。

{{<mermaid align="center">}}
graph LR
	A[mbtiles] --> B{対象エリアは大きいですか?}
  B -->|いいえ|C[narwassco/vt-map]
	B -->|はい|D[wasac/vt]
  C -->|ローカルでタイルを生成します|E[gh-pages]
  D -->|mbtilesをアップロード|F[github masterブランチ]
  F -->|Github Actionsでタイルを生成します|E
{{< /mermaid >}}

### i. [narwassco/vt-mapアプローチ] ケニアのナロックウォーターの場合
もし対象エリアが狭い場合は、`ナロックウォーター`のアプローチでデプロイすることができます。次のリポジトリを参照してください。

- [narwassco/vt-map](https://github.com/narwassco/vt-map)
  これは次のモジュールを使用してMapboxベクトルタイルを生成し、gh-pagesにデプロイします。
  - [watergis/postgis2mbtiles](https://github.com/watergis/postgis2mbtiles): PostGISから`mbtiles`を生成します。
  - [watergis/mbtiles2pbf](https://github.com/watergis/mbtiles2pbf): `mbtiles`を`pbf(mvt)`タイルに変換します。

このモジュールは[mapbox/tippecanoe](https://github.com/mapbox/tippecanoe)を使用してmbtilesを生成します。しかしながら、ナロックウォーターのGISマシンはWindows10 Proのため、`tippecanoe`の実行が困難であり、`Docker`を使用してベクトルタイルを生成するツールを開発しました。

### ii. [WASAC/vtアプローチ] ルワンダのWASACの場合 (推奨)
もし対象エリアが広い場合は、Github pagesに数千のベクトルタイルをデプロイすることは容易ではないでしょう。`WASAC`のアプローチを使って、`mbtiles`を先にアップロードした後、`Github Actions`で`mbtiles`からベクトルタイルを取り出すと良いです。次に示すリポジトリをご覧になってください。

- [WASAC/vt](https://github.com/WASAC/vt)
  これは次のモジュールを使用してMapboxベクトルタイルを生成し、gh-pagesにデプロイします。
  - [watergis/postgis2mbtiles](https://github.com/watergis/postgis2mbtiles): PostGISから`mbtiles`を生成します。 `postgis2mbtiles`モジュールはローカルマシンに実行します。 
  - [watergis/mbtiles2pbf](https://github.com/watergis/mbtiles2pbf): `mbtiles`を`pbf(mvt)`タイルに変換します。 `mbtiles2pbf`は`Github Actions`で実行します。

次のものは`ナロックウォーター`が使用している`Github Actions`でmbtilesタイルからpbfタイルを生成しデプロイするためのワークフローファイルです。

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

- `ナロックウォーター`も[`narwassco/vt-map`アプローチ]の代わりに、[`WASAC/vt`アプローチ]を使い始めました。 
  - [narwassco/vt](https://github.com/narwassco/vt)

- `ナクルウォーター`も[`WASAC/vt`アプローチ]を使い始めました。
  - [nakuruwater/vt](https://github.com/nakuruwater/vt)