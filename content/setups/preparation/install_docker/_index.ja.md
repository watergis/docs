---
title: Dockerのインストール
weight: 13
---

このツールキットは`tippecanoe`というツールを使うために`Docker`を使用してPostGISデータベースからベクトルタイルを生成します。したがってコンピュータには`Docker`をインストールする必要があります。 

#### Docker Desktop（Windows）
[公式ウェブサイト](https://docs.docker.com/docker-for-windows/install/)を参照し、インストールしてください。

- インストールする際には`Linuxコンテナ`を選択してください(`Windowsコンテナ`ではありません!)
- Hyper-Vを有効にする必要があります。

#### Docker Desktop（MacOS）
[公式ウェブサイト](https://docs.docker.com/docker-for-mac/)を参照し、`Homebrew`でインストールしてください。

```bash
brew search docker
brew cask install docker
```

#### Docker（Ubuntu）
[公式ウェブサイト](https://docs.docker.com/engine/install/ubuntu/)を参照し、インストールしてください。

