---
title: Develop and Deploy Web Application
weight: 26
---

You can use [Mapbox GL JS](https://docs.mapbox.com/mapbox-gl-js/api/) to develop your own web application and delopy it to gh-pages. 

## Use boilerplate to create your repository
[watergis/mapboxgljs-boilerplate](https://github.com/watergis/mapboxgljs-boilerplate) is the template of Mapbox GL JS implementation for Water Services Providers with all of customized plugins. You can use this template to create your own repository easily.

## Fork an existing repository to your organization
It is also possible for you to fork our water services providers' application.

- `Narok Water and Sewerage Services Co., Ltd, KENYA` : [narwassco/mapbox-gl-js-client](https://github.com/narwassco/mapbox-gl-js-client) 
- `Water and Sanitation Corporation, Ltd, RWANDA` : [WASAC/mapbox-gl-js-client](https://github.com/WASAC/mapbox-gl-js-client) 
- `Nakuru Water and Sanitation Services Co., Ltd, KENYA` : [nakuruwater/mapbox-gl-js-client](https://github.com/nakuruwater/mapbox-gl-js-client) 

### Customized Mapbox GL JS Plugins for this toolkit.

I developed the following plugins for the web application for water services providers. All the plugins are already included in `mapbox-gl-js-client` repository for `Narok Water` and `WASAC`.
- [watergis/mapbox-gl-export](https://github.com/watergis/mapbox-gl-export)
- [watergis/mapbox-gl-legend](https://github.com/watergis/mapbox-gl-legend)
- [watergis/mapbox-gl-area-switcher](https://github.com/watergis/mapbox-gl-area-switcher)
- [watergis/mapbox-gl-pitch-toggle-control](https://github.com/watergis/mapbox-gl-pitch-toggle-control)
- [watergis/mapbox-gl-popup](https://github.com/watergis/mapbox-gl-popup)

### Automating deployment process for web application
Both Narok water and WASAC's applications are using Github Action to deploy the application to gh-pages automatically. You can also use Circle CI or Github Actions to automate.

Github Action's workflow file is [here](https://github.com/narwassco/mapbox-gl-js-client/blob/master/.github/workflows/node.js.yml). You also need to register environmental variable on secret page on setting. 

- `ACCESSTOKEN` : Your Mapbox Access Token
- `CNAME` : Your custom domain like `narok.water-gis.com`. If you don't have own domain, you don't need to put `CNAME`.

The below is an example of Github Action's workflow file

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
