# Add SSL with Let's Encrypt

We have a site that we want to add SSL to.


Install `nginx` and all the dependencies for Let's Encrypt:

```
# apt install nginx python3-acme python3-certbot python3-mock python3-openssl python3-pkg-resources python3-pyparsing python3-zope.interface
# apt install python3-certbot-nginx
```

Reload `nginx`:

```
# systemctl reload nginx
```

Assume an existing config file:

```
# cat /etc/nginx/sites-available/proxy
server {
  server_name test.famicoman.com;
  listen 80;
  
  auth_basic "Administrator’s Area";
  auth_basic_user_file /etc/nginx/.htpasswd;

  location / {
    proxy_pass http://10.10.10.20:8080;
    include proxy_params;
  }
}
```

Run `certbot` to generate the certificate:

```
# certbot --nginx -d test.famicoman.com
```

Check the config file to observe the changes:

```
# cat /etc/nginx/sites-available/test.famicoman.com
server {

  server_name test.famicoman.com;

  auth_basic "Administrator’s Area";
  auth_basic_user_file /etc/nginx/.htpasswd;

  location / {
    proxy_pass http://10.10.10.20:8080;
    include proxy_params;
  }

    listen [::]:443 ssl ipv6only=on; # managed by Certbot
    listen 443 ssl; # managed by Certbot
    ssl_certificate /etc/letsencrypt/live/test.famicoman.com/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/test.famicoman.com/privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot

}
server {
    if ($host = test.famicoman.com) {
        return 301 https://$host$request_uri;
    } # managed by Certbot


  listen 80;
  listen [::]:80;

  server_name test.famicoman.com;
    return 404; # managed by Certbot


}
```

Restart `nginx`:

```
# systemctl restart nginx
```

Make sure there is a hole in the firewall for port `443` (HTTPS) and optionally drop traffic on port `80` (HTTP):

```
# cat /etc/iptables/rules.v4 | grep 443
-A INPUT -p tcp -m tcp --dport 443 -j ACCEPT
# cat /etc/iptables/rules.v4 | grep 80
-A INPUT -p tcp -m tcp --dport 80 -j DROP
```