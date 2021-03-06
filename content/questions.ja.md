---
title: Q&A
disableToc: true
---

#### 1. どうやってパイプのサイズを変えますか?
ベクトルタイル経由でデータの編集をすることはできません。ベクトルタイルは静的データであるがゆえに、スムーズな地図データへのアクセスを実現しています。QGISやArcGISなどのデスクトップGISを用いてデータの更新をしていく必要があります。

---
#### 2. ベクトルタイルでどうやってNRWを削減できますか?
実際のところ、まだ良い参考例がありません。しかしながら、もし全ての職員と広くGISデータを共有できたなら、NRWの管理の効率化に寄与することでしょう。

ところで、実はこのWebGISアプリにEPANETの機能を追加できないかと検討をいましています。もしEPANETでの解析結果を容易に見れたら大きく寄与できると思います。

---
#### 3. ベクトルタイルについてよく理解できていませんが、ベクトルタイルデータを作るには元になるソースデータは何らかのデータベースに入れておかないといけないのでしょうか？
その通りです。GISデータをあらかじめ何らかのGISデータベースに格納しておく必要があります。このツールはGISデータベースから直接ベクトルタイルを作成します。PostgreSQL/PostGISはオープンソースであるのでこのアプローチではPostGISを使用しています。しかしながら、もしSQL ServerやOracleなどの他のデータベースを使っている場合は、ソースコードを修正して使えるようにすることもできるでしょう。

---
#### 4. オフラインで使えますか？Maps.meみたいにスマホやPCにダウンロードして閲覧できますか？
残念ながら、オンラインのアプリなのでオフラインで見ることはできません。しかしながらmbtilesタイルセットをAndoridデバイスにダウンロードすることで、QFieldやINPUTなどのアプリを介してオフラインで見ることは可能になります。

---
#### 5. ベクトルタイルをどのように水道管網の開発プロジェクトに活用できますか？
ルワンダではベクトルタイルに統計データなども含めています。そうすることで全ての職員が水道施設計画などに必要な既存の情報を閲覧でき、将来的な開発計画に活用できます。 

---
#### 6. QGISごしにベクトルタイルを使う利点は何ですか？
多くの水道局のGIS担当者は実際に編集機能について尋ねてきます。しかし、WebGISに編集機能を組み入れると現実的なコストではなくなります。このアプローチでは編集機能は全てQGIS側に任せています。そうすることでシンプルなGUIを実現し、他の人にも容易に使ってもらえます。また開発やトレーニングにかかるコストも抑えられます。

---
#### 7. オープンデータにすることでプライバシーなどの問題が起こり得ます。どのように解決しますか？
その通りだと思います。もし何らかのデータをオープンにしたときに、ごくまれにリスクになることがあります。そのため、どういったデータをオープンデータとして公開していいのか考慮しなければなり真s年。ルワンダでは顧客名などのプライバシーデータは基本削除しました。ナロックウォーターではセキュリティ的な理由で顧客名による検索機能を削除しました。自分たちのベクトルタイルをデザインする際に、どういったデータを公開するのかよく議論するべきです。

---
#### 8. Googleマップをベースマップとして使えますか？I
いいえ、グーグルマップを使うことはできません。グーグルマップはライセンスに非常に厳しく、また使用には多額の利用料が伴います。しかしながら、このツールはMapboxやMaptilerや国連ベクトルタイルが提供するOpenStreetMapベースの地図を使うことができます。またあなた自身の持っているデータをOSMの上にオーバーレイして使うこともできます。例えばルワンダとケニアでは土地局の筆ポリゴンデータを独自にOSMの上に追加しています。筆ポリゴンデータは多くの水道局にとって新規接続などする際にとても役に立つでしょう。
