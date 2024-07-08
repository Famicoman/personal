# Set Up A Password-Protected Directory

We have a site that we want to hide behind basic auth with a username/password.


Install `nginx` and `apache2-tools`:

```
# apt install nginx apache2-tools
```

Create a new site config file:

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

Note that the root of this site will proxy to `http://10.10.10.20:8080` which is our target machine.

Now we need to create the basic auth user file using `-c` to create (updates for the same user can be done without this flag) and `-B` to specify bcrypt for the password hashing algorithm:

```
#  htpasswd -c -B /etc/ntinx/.htpasswd famicoman
```

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

Make sure there is a hole in the firewall for our new proxy:

```
# cat /etc/iptables/rules.v4 | grep 80
-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT
```