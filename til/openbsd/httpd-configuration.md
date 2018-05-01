# httpd Configuration

OpenBSD comes with its own webserver, `httpd`. You don't need to install anything further if you intend on hosting a static site. 

As root, create a new `httpd.conf` file in `/etc/` or copy an example from `/etc/examples/httpd.conf`:

```
# vi /etc/httpd.conf
```

Paste the following, editing anything as needed and save when done:

```
# $OpenBSD: httpd.conf

#
# Macros
#
ext_addr="*"


#
# Servers
#

# A minimal default server
server "default" {
        listen on $ext_addr port 80
		# I don't think root is needed here, but it might be
		# Default root is seemingly /var/www/htdocs/
        root "/htdocs"
}

## Uncomment to host a site, example.com
# server "example.com" {
#   listen on $ext_addr port 80
#   root "/htdocs/example.com"
# }


# Include MIME types instead of the built-in ones
types {
        include "/usr/share/misc/mime.types"
}
```

Now, let's make an `index.html` file to test with:

```
# vi /var/www/htdocs/index.html
```

Paste the following and save the file:

```
<html>
	<body>
		Hello World!
	</body>
</html>
```

Next, check the configuration to make sure it is valid:

```
# httpd -n
configuration OK
```

Finally enable and start `httpd` using `rcctl`:

```
# rcctl enable httpd
# rcctl start httpd
```

`rcctl` modifies `/etc/rc.conf.local`, overriding `/etc/rc.conf` to enable the daemon and then flip it on.

We can test if our server is functioning by loading the machine's IP address in a browser. If you don't want to access the web page on the same machine, use `ifconfig` to get the IP address.

## Sources
* https://www.romanzolotarev.com/openbsd/webserver.html
* http://thecyberrecce.net/2017/01/15/secure-webservers-with-openbsd-6-0-setting-up-httpd-mariadb-and-php/