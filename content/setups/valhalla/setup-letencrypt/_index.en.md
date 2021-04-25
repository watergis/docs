---
title: Setup Let's Encrypt to enable SSL
weight: 42
---

Now you will be able to use Valhalla, but it is better to enable SSL in order to secure the connection. We are going to setup let's encrypt to enable SSL by using your own domain.

Here, we use `valhalla.water-gis.com` domain for Valhalla API.

## Create A record on your DNS Server

The below image is an example on Google Domain.

![image](https://user-images.githubusercontent.com/2639701/115984536-85263e00-a5e2-11eb-8587-68e18d6e146b.png)


## Setup of Nginx and certbot

```bash
$ sudo apt install certbot python3-certbot-nginx
$ sudo mkdir -p /var/www/valhalla.water-gis.com/html
$ sudo chown -R $USER:$USER /var/www/valhalla.water-gis.com/html
$ sudo chmod -R 755 /var/www/valhalla.water-gis.com
$ vi /var/www/valhalla.water-gis.com/html/index.html
```

`index.html` should be as below.
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

Test your default index.html
```bash
$ curl http://valhalla.water-gis.com
```

## Reverse proxy to valhalla API
```bash
$ sudo vi /etc/nginx/sites-available/valhalla.water-gis.com
```

`valhalla.water-gis.com` should be as below.
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
# create shortcut
$ sudo ln -s /etc/nginx/sites-available/valhalla.water-gis.com /etc/nginx/sites-enabled/
# edit nginx.conf if necessary
$ sudo vi /etc/nginx/nginx.conf

# restart nginx
$ sudo nginx -t
$ sudo systemctl restart nginx
```

By this step, it will work without SSL. In the next step, we are going to configure let's encrypt.

## Enable SSL

```bash
$ sudo certbot --nginx -d valhalla.water-gis.com
```

- logs
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

If you access the above URL(https://www.ssllabs.com/ssltest/analyze.html?d=valhalla.water-gis.com) from let's encrypt, you will see the following result.

![image](https://user-images.githubusercontent.com/2639701/115983271-3032f980-a5db-11eb-874e-3f274bf3e638.png)

now, restart nginx to enable SSL.
```bash
sudo nginx -t
sudo systemctl restart nginx
```

Open `https://valhalla.water-gis.com` in your browser. You will see the response from valhalla API. Now, your valhalla works with SSL!

## References

- https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-20-04#step-5-–-setting-up-server-blocks-(recommended)
- https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-20-04-ja https://qiita.com/kga/items/e30d668ec1ac5e30025b