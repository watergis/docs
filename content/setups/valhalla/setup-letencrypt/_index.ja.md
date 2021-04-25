---
title: Let's EncryptでSSL化
weight: 42
---

これでValhallaが使えるようになりますが、接続を安全にするためにはSSLを有効にした方が良いでしょう。ここでは、独自のドメインを使ってSSLを有効にするために、let's encryptを設定します。

ここでは、Valhalla APIに`valhalla.water-gis.com`ドメインを使用しています。

## DNSサーバーにAレコードを作成

下の画像は、Google Domainでの例です

![image](https://user-images.githubusercontent.com/2639701/115984536-85263e00-a5e2-11eb-8587-68e18d6e146b.png)


## Nginxとcertbotのセットアップ

```bash
$ sudo apt install certbot python3-certbot-nginx
$ sudo mkdir -p /var/www/valhalla.water-gis.com/html
$ sudo chown -R $USER:$USER /var/www/valhalla.water-gis.com/html
$ sudo chmod -R 755 /var/www/valhalla.water-gis.com
$ vi /var/www/valhalla.water-gis.com/html/index.html
```

`index.html`は以下のようになるでしょう。
```html
<html>
    <head>
        <title>Welcome to valhalla.water-gis.com!</title>
    </head>
    <body>
        <h1>Success!  The valhalla.water-gis.com server block is working!</h1>
    </body>
</html>
```

index.htmlが表示されるか確認します。
```bash
$ curl http://valhalla.water-gis.com
```

## valhalla APIへのリバースプロキシ
```bash
$ sudo vi /etc/nginx/sites-available/valhalla.water-gis.com
```

`valhalla.water-gis.com`ファイルは以下のようになるでしょう。
```conf
server {
        listen 80;
        listen [::]:80;

        root /var/www/valhalla.water-gis.com/html;
        index index.html index.htm index.nginx-debian.html;

        server_name valhalla.water-gis.com;
        
        location / {
                proxy_pass http://localhost:8002;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header Host $host;
                proxy_redirect off;
        }
}
```

```bash
# シンボリックリンクの作成
$ sudo ln -s /etc/nginx/sites-available/valhalla.water-gis.com /etc/nginx/sites-enabled/
# 必要であれば nginx.conf を編集
$ sudo vi /etc/nginx/nginx.conf

# Nginx再起動
$ sudo nginx -t
$ sudo systemctl restart nginx
```

この手順で、SSLなしでも動作するようになります。次のステップでは、let's encryptの設定を行います。

## SSLの有効化

```bash
$ sudo certbot --nginx -d valhalla.water-gis.com
```

- ログ
```bash
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Congratulations! You have successfully enabled https://valhalla.water-gis.com

You should test your configuration at:
https://www.ssllabs.com/ssltest/analyze.html?d=valhalla.water-gis.com
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

IMPORTANT NOTES:
 - Congratulations! Your certificate and chain have been saved at:
   /etc/letsencrypt/live/valhalla.water-gis.com/fullchain.pem
   Your key file has been saved at:
   /etc/letsencrypt/live/valhalla.water-gis.com/privkey.pem
   Your cert will expire on 2021-07-04. To obtain a new or tweaked
   version of this certificate in the future, simply run certbot again
   with the "certonly" option. To non-interactively renew *all* of
   your certificates, run "certbot renew"
 - If you like Certbot, please consider supporting our work by:

   Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
   Donating to EFF:                    https://eff.org/donate-le
```

let's encryptから上記のURL(https://www.ssllabs.com/ssltest/analyze.html?d=valhalla.water-gis.com)にアクセスすると、以下のような結果になります。

![image](https://user-images.githubusercontent.com/2639701/115983271-3032f980-a5db-11eb-874e-3f274bf3e638.png)

ここで、nginxを再起動してSSLを有効にします。
```bash
sudo nginx -t
sudo systemctl restart nginx
```

ブラウザで`https://valhalla.water-gis.com`を開きます。valhalla APIからのレスポンスが表示されました。これで、valhallaのSSL化ができました。

## 参考にしたウェブサイト

- https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-20-04#step-5-–-setting-up-server-blocks-(recommended)
- https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-20-04-ja https://qiita.com/kga/items/e30d668ec1ac5e30025b