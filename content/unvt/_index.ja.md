---
title: UNVTとの統合
weight: 70
pre: "<b>7. </b>"
chapter: true
---

### 第７章

この章では[国連ベクトルタイルツールキット (UNVT)](https://github.com/unvt)を用いてOSMベースの完全にフリーな地図を作る方法を示します。ルワンダとケニアでは、オープンストリートマップから作れる完全にライセンスフリーな地図としてUNVTをベースマップの一つとして使っています。

もし、GoogleマップやMapbox、Maptilerやそのほかの地図プロバイダへの支払いを減らしたいのでしたら、UNVTはまさにうってつけと言えるでしょう。

#### Github pagesで一つの国のUNVTマップをホストする

UNVTは主にRaspberry Piでのオペレーションを想定していますが、Github pagesにホストして、ベクトルタイルを配信することも可能です。UNVTは高速にそして軽いベクトルタイルを生産できます。

Github pagesにホストするためには、[unvt/naru](https://github.com/unvt/naru)というリポジトリを活用します。

ここではDockerを使った生産方法を紹介します。

##### 1. unvt/naruをフォークする

まず[unvt/naru](https://github.com/unvt/naru)をGithubでフォークします。

##### 2. セットアップ

最初にマシン（Windows, MacOS, Linux）にDockerをインストールします。[こちら](https://docs.docker.com/get-docker/)のガイドをご覧ください。

それから、Githubからソースコードをダウンロードし、Dockerイメージをビルドします。
```zsh
git clone https://github.com/{your organization name}/naru.git
cd naru
docker build . --tag unvt/naru
```

##### 3. ベクトルタイルの生産

```zsh
cd naru
docker run -v $(pwd):/usr/src/app -p 9966:9966 -it unvt/naru
# ここからDockerコンテナに入ります
cd /usr/src/app
cp .env.example .env
vi .env # 環境変数を編集します
 ```

ここでは、東アフリカのルワンダ向けのUNVTマップを生産していきます。[Geofabrik](http://download.geofabrik.de)で指定するリージョンとエリアを確認できます。

次は`.env`の設定例です。
```
REGION=africa
AREA=rwanda
SITE_ROOT=http://localhost:9966
```

さて、次に示す一連のコマンドを実行して、ベクトルタイルに必要なコンポーネントを生成していきます。

```zsh
rake inet:download # osm.pbfをダウンロード
rake inet:mbgljs # mapbox-gl-js パッケージをダウンロード
rake js # JavaScriptコードをロールアップ
rake inet:sprite # makiアイコンのダウンロードとスプライトファイルの作成
rake inet:fonts # フォントのダウンロードとGlyphの作成
rake tiles # タイルの生成
rake style # style.jsonの生成
```

上のコマンドを実行すると、全てのリソースが`docs`フォルダに作成されます。`docs`は主にGithub pagesで公開する際に使用されます。

`docs`フォルダの構成は下のようになっているでしょう。
- docs
  - glyphs
  - js
    - bundle.js
    - bundle.js.map
    - mapbox-gl.css
    - mapbox-gl.js
  - sprite
    - sprite.json
    - sprite.png
    - sprite@2x.json
    - sprite@2x.png
    - sprite@4x.json
    - sprite@4x.png
  - zxy
  - glyphs.json 
  - index.html
  - style.json

これで、ローカルブラウザで地図をチェックする用意が整いました！

下のコマンドを実行して、`budo`でホストします。
```
rake host
```

[http://localhost:9966](http://localhost:9966)をブラウザで開いてUNVTマップを確認します。

##### 4. Githubへのタイルのアップロード

もしUNVTマップが問題なければ、Githubにアップロードして公開します。

```zsh
git add docs -f  # we use -f option to force to commit all documents
git commit -m "generated vectortiles"
git push origin master
```

##### 5. `docs`フォルダをGithub pagesとして公開する

`settings` of your `naru`リポジトリのページの`settings`に行って、`Options`タブから`Github Pages`セクションを見つけます。そこでGithub pagesの設定ができます。

さらに詳細な情報は[こちら](https://docs.github.com/en/github/working-with-github-pages/about-github-pages)の公式サイトをご覧ください。

Github pagesで公開したあとは、`https://{your organization}.github.io/naru`のようなURLでUNVTマップを閲覧できます。

また、次に示す全てのコンポーネントにもアクセスできます。

- ベクトルタイル
```
https://{your organization}.github.io/naru/zxy/{z}/{x}/{y}.pbf
```

- Spriteファイル
```
https://{your organization}.github.io/naru/sprite/sprite
```

- Glyphs
```
https://{your organization}.github.io/naru/glyphs/{fontstack}/{range}.pbf
```

#### より高度な設定

##### a. 低縮尺0-5レベル用にNatural Earthマップを統合する

UNVTのOSMマップはズームレベルの6 - 15しか生成しません。もし低縮尺の地図が必要ならUNVTベースのNatural Earthを追加できます。

Natural Earthマップを追加するためには、リポジトリの`Rakefile`を編集する必要があります。

  - `rake inet:download` セクション

  ```ruby
  desc 'download source geospatial data to the place'
  task :download do
    if !File.exist?("src/#{AREA}-latest.osm.pbf")
      u = "https://download.geofabrik.de/#{REGION}/{#{AREA}-latest.osm.pbf}"
      sh "curl -C - #{u} --output './src/#1'"
    end
    # 次のコマンドを追加します
    if !File.exist?("src/ne_tiles.mbtiles")
      u = "https://watergis.github.io/unvt-ne/{ne_tiles.mbtiles}"
      sh "curl -C - #{u} --output './src/#1'"
    end
  end
  ```

  - `rake tiles` セクション
  ```ruby
  desc 'build tiles from source data'
  task :tiles do
    sh "osmium export --config osmium-export-config.json --index-type=sparse_file_array --output-format=geojsonseq --output=- src/#{AREA}-latest.osm.pbf | node filter.js | tippecanoe --no-feature-limit --no-tile-size-limit --force --simplification=2 --maximum-zoom=15 --base-zoom=15 --hilbert --output=#{MBTILES}"
    # tile-join tiles.mbtiles と ne_tiles.mbtilesをtile-joinします
    sh "tile-join --force --no-tile-compression --output-to-directory=docs/zxy --no-tile-size-limit #{MBTILES} src/ne_tiles.mbtiles"
  end
  ```

  - Natural Earthレイヤ用のスタイルを追加する。
  Natural Earthレイヤ用のスタイルを追加する必要があります。この[リポジトリ](https://github.com/WASAC/naru/tree/develop/hocon)を利用することができます。ファイル名の先頭が`ne-`で始まるスタイルがNatural Earthレイヤとなっています。

  もし難しければ、`WASAC/naru`リポジトリの`hocon`フォルダから単純にコピーしてくるだけでも良いでしょう。

##### b. Github Actionsを使用したタイルデータ更新の自動化

[WASAC/naru](https://github.com/WASAC/naru)ではGithub Actionを使用してUNVTのデータを自動更新しています。

同じワークフローファイルを使うことができます。

[deploy.yaml](https://github.com/WASAC/naru/blob/develop/.github/workflows/deploy.yml). このファイルを使うことで毎月1日と15日に2週間おきにデータを更新します。
```yaml
name: deploy

on:
  # push:
  #   branches: [ develop ]

  schedule:
    - cron:  '0 0 1,15 * *'

jobs:

  deploy:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - name: Generate tiles
      env:
        REGION: africa
        AREA: rwanda
        SITE_ROOT: https://wasac.github.io/naru
      run: |
        docker-compose up
    - name: Use Node.js
      uses: actions/setup-node@v1
      with:
        node-version: 12.x
    - run: yarn
    - name: configure git and deploy
      env:
        NODE_AUTH_TOKEN: ${{secrets.GITHUB_TOKEN}}
        # 広い面積の国のタイルを生成する際には下のオプションがいるかもしれません
        NODE_OPTIONS: "--max-old-space-size=8192"
      run: |
        git config --global user.name "{your organization name}+githubci"
        git config --global user.email "{your organization name}+githubci@users.noreply.github.com"
        git remote set-url origin https://x-access-token:${NODE_AUTH_TOKEN}@github.com/{your organization name}/naru.git
        yarn run deploy
```
