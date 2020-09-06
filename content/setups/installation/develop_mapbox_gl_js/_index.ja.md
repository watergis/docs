---
title: ウェブアプリの開発とデプロイ
weight: 26
---

[Mapbox GL JS](https://docs.mapbox.com/mapbox-gl-js/api/)を使ってあなた自身のウェブアプリを開発して、gh-pagesにデプロイします。

## ボイラープレートを使ってリポジトリを作る
[watergis/mapboxgljs-boilerplate](https://github.com/watergis/mapboxgljs-boilerplate)はMapbox GL JSを既に導入済みのテンプレートであり、水道事業体向けの全てのカスタマイズされたプラグインを含んでいます。このテンプレートを使うことで容易にあなた自身のリポジトリを作成できます。 

## 既存のリポジトリをあなたの組織にフォークする
既存の水道事業体のアプリをフォークすることも可能です。

- `Narok Water and Sewerage Services Co., Ltd, KENYA` : [narwassco/mapbox-gl-js-client](https://github.com/narwassco/mapbox-gl-js-client) 
- `Water and Sanitation Corporation, Ltd, RWANDA` : [WASAC/mapbox-gl-js-client](https://github.com/WASAC/mapbox-gl-js-client) 
- `Nakuru Water and Sanitation Services Co., Ltd, KENYA` : [nakuruwater/mapbox-gl-js-client](https://github.com/nakuruwater/mapbox-gl-js-client) 

### このツールキット用にカスタマイズされたMapbox GL JSプラグイン

水道事業体向けのアプリのために次のプラグインを開発しました。全てのプラグインは`ナロックウォーター`と`WASAC`のために`mapbox-gl-js-client`に含まれています。
- [watergis/mapbox-gl-print](https://github.com/watergis/mapbox-gl-print)
- [watergis/mapbox-gl-legend](https://github.com/watergis/mapbox-gl-legend)
- [watergis/mapbox-gl-area-switcher](https://github.com/watergis/mapbox-gl-area-switcher)
- [watergis/mapbox-gl-pitch-toggle-control](https://github.com/watergis/mapbox-gl-pitch-toggle-control)
- [watergis/mapbox-gl-popup](https://github.com/watergis/mapbox-gl-popup)

### ウェブアプリのデプロイプロセスの自動化
ナロックウォーターとWASACのアプリではGithub Actionを使用してgh-pagesへのデプロイを自動化しています。Circle CIやGithub Actionを使用した自動化をすることが可能です。

Github Actionのワークフローファイルは[こちら](https://github.com/narwassco/mapbox-gl-js-client/blob/master/.github/workflows/node.js.yml)にあります。設定の中のシークレットページで次の環境変数の登録もする必要があります。 

- `ACCESSTOKEN` : Mapboxのアクセストークン
- `CNAME` : `narok.water-gis.com`のようなカスタムドメイン。自身のドメインを持っていない場合は`CNAME`は不要です。

次のはGithub Actionのワークフローファイルのサンプルです。

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
    - name: configure git, build and deploy
      env:
        NODE_AUTH_TOKEN: ${{secrets.GITHUB_TOKEN}}
        ACCESSTOKEN: ${{secrets.ACCESSTOKEN}}
        CNAME: ${{secrets.CNAME}}
      run: |
        echo "ACCESSTOKEN=${ACCESSTOKEN}" > .env
        echo "CNAME=${CNAME}" >> .env
        npm run build
        git config --global user.name "narwassco+githubci"
        git config --global user.email "narwassco+githubci@users.noreply.github.com"
        git remote set-url origin https://x-access-token:${NODE_AUTH_TOKEN}@github.com/narwassco/mapbox-gl-js-client.git
        npm run deploy
```