---
title: Intergration with UNVT
weight: 70
pre: "<b>7. </b>"
chapter: true
---

### Chapter 7

This chapter will show how you can establish completely free OSM based map by using [United Nations Vector Tiles Toolkits (UNVT)](https://github.com/unvt). In Rwanda and Kenya, we are using UNVT as one of base maps which is completeley license free's map generated from Open Street Map.

If you are suffering for the payment for Google Map, Mapbox, Maptiler or any other map services providers, UNVT would be the great tool for your organization.

#### Hosting UNVT map for a country on Github pages

UNVT is mainly designed for operating on Raspberry Pi, however it can be hosted on Github pages to distribute OSM based vactor tiles. It can produce vector tiles very fast and lightly.

For hosting on Github pages, you can use [unvt/naru](https://github.com/unvt/naru) respository.

Here, I introduce how to generate by using Docker.

##### 1. Fork unvt/naru

Firstly, you can fork [unvt/naru](https://github.com/unvt/naru) on your Github.

##### 2. Setup

Firstly, you can install Docker and docker-compose on your computer either Windows, MacOS or Linux. See the instruction [here](https://docs.docker.com/get-docker/).

Then, you can download the source code from Github, and build Docker image.
```zsh
git clone https://github.com/{your organization name}/naru.git
cd naru
docker build . --tag unvt/naru
```

##### 3. Generate vector tiles

```zsh
cd naru
docker run -v $(pwd):/usr/src/app -p 9966:9966 -it unvt/naru
# now you entered into Docker container
cd /usr/src/app
cp .env.example .env
vi .env # edit environmental variable
 ```

Here, we are going to generate UNVT map for Rwanda in Easern Africa. You can confirm the region and area on [Geofabrik](http://download.geofabrik.de).

The below is an example of `.env`.
```
REGION=africa
AREA=rwanda
SITE_ROOT=http://localhost:9966
```

 Now, you execute the following commands to generate each components for vector tiles map.

```zsh
rake inet:download # download osm.pbf
rake inet:mbgljs # download mapbox-gl-js package
rake js # rollup javascript code
rake inet:sprite # download maki and build sprite
rake inet:fonts # download fonts and create glyphs
rake tiles # create mbtiles under src folder
rake style # create style.json
```

After running the above commands, all of resources will be created under `docs` folder. `docs` folder is normally used for Github pages public directory.

the structure of `docs` directory should be as below.
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

Now you can ready to check your map on local browser!

Just run the below command to host tiles by `budo`.
```
rake host
```

open [http://localhost:9966](http://localhost:9966) on your browser to check your UNVT map.

##### 4. Uploading tiles to Github

If your UNVT map's everything is okay, you can now upload it to Github for publishing.

```zsh
git add docs -f  # we use -f option to force to commit all documents
git commit -m "generated vectortiles"
git push origin master
```

##### 5. Make `docs` folder publish as Github pages

Go to `settings` of your `naru` repository page, then you can find `Github Pages` section on `Options` tab. You can configure github pages there.

Please also see more detailed information on their public website [here](https://docs.github.com/en/github/working-with-github-pages/about-github-pages).

After publishing as Github pages, you can access your UNVT map from the URL like `https://{your organization}.github.io/naru`.

Also, you can access your all components of map as following.

- Vector Tiles
```
https://{your organization}.github.io/naru/zxy/{z}/{x}/{y}.pbf
```

- Sprite file
```
https://{your organization}.github.io/naru/sprite/sprite
```

- Glyphs
```
https://{your organization}.github.io/naru/glyphs/{fontstack}/{range}.pbf
```

#### Advanced development

##### a. Interageration Natural Earth Map for low scale zoom levels 0 - 5

UNVT's OSM map only generate zoom level 6 to 15. If you need low scale map, you can add Natural Earth based UNVT.

In order to add Natural Earth Map, you need to modify `Rakefile` in your repository.

  - `rake inet:download` section

  ```ruby
  desc 'download source geospatial data to the place'
  task :download do
    if !File.exist?("src/#{AREA}-latest.osm.pbf")
      u = "https://download.geofabrik.de/#{REGION}/{#{AREA}-latest.osm.pbf}"
      sh "curl -C - #{u} --output './src/#1'"
    end
    # add the below command.
    if !File.exist?("src/ne_tiles.mbtiles")
      u = "https://watergis.github.io/unvt-ne/{ne_tiles.mbtiles}"
      sh "curl -C - #{u} --output './src/#1'"
    end
  end
  ```

  - `rake tiles` section
  ```ruby
  desc 'build tiles from source data'
  task :tiles do
    sh "osmium export --config osmium-export-config.json --index-type=sparse_file_array --output-format=geojsonseq --output=- src/#{AREA}-latest.osm.pbf | node filter.js | tippecanoe --no-feature-limit --no-tile-size-limit --force --simplification=2 --maximum-zoom=15 --base-zoom=15 --hilbert --output=#{MBTILES}"
    # You need to tile-join tiles.mbtiles and ne_tiles.mbtiles
    sh "tile-join --force --no-tile-compression --output-to-directory=docs/zxy --no-tile-size-limit #{MBTILES} src/ne_tiles.mbtiles"
  end
  ```

  - add style for Natural Earth layers
  You need to add style for additional natural earth layers. You can use the style from this [repository](https://github.com/WASAC/naru/tree/develop/hocon). I indicated the file name start with `ne-` as Natural Earth layers.

  If you think it is difficult, just simply copy `hocon` folder from `WASAC/naru` repository.

##### b. Automate to update tiles data by using Github Actions

[WASAC/naru](https://github.com/WASAC/naru) repository is fully adopted Github Actions to automate updating OSM data.

You can use the same workflow file for your repository.

[deploy.yaml](https://github.com/WASAC/naru/blob/develop/.github/workflows/deploy.yml). This yaml is for updating every two weeks on 1st and 15th each month.
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
        # below option might be required for large area of the country's map
        NODE_OPTIONS: "--max-old-space-size=8192"
      run: |
        git config --global user.name "{your organization name}+githubci"
        git config --global user.email "{your organization name}+githubci@users.noreply.github.com"
        git remote set-url origin https://x-access-token:${NODE_AUTH_TOKEN}@github.com/{your organization name}/naru.git
        yarn run deploy
```
