# Set Up A Reverse Proxy

There is a device on our network running a web server that we want to make available elsewhere. We will set up `nginx` as a reverse proxy on the same network segment so that and queries to `nginx` are relayed transparently to the actual target machine.

Install `nginx`:

```
# apt install nginx
```

Create a new site config file:

```
# cat /etc/nginx/sites-available/proxy
server {
  listen 10.10.10.20:8080;

  location / {
    proxy_pass http://192.168.3.100;
    include proxy_params;
  }
}
```

Note that we are listening on `10.10.10.20` which is the IP address our machine gets for a VPN. Port `8080` is a nonstandard port we will be listening on. The root of this site will proxy to `http://192.168.3.100` which is our target machine.

Now link this config into `sites-enabled`:

```
# ln -s /etc/nginx/sites-available/proxy /etc/nginx/sites-enabled/proxy
```

Test the config to check for issues:

```
# nginx -t
```

Restart `nginx`:

```
# systemctl restart nginx
```

Make sure there is a hole in the firewall for our new proxy (note that `wg0` is the interface for our VPN connection):

```
# cat /etc/iptables/rules.v4 | grep 8080
-A INPUT -i wg0 -p tcp -m tcp --dport 8080 -j ACCEPT
```

## Sources
* https://randyzwitch.com/mirror-ftp-lftp/
* http://root42.blogspot.com/2013/09/how-to-get-directory-recursively-with.html