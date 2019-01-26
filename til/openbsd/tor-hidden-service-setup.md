# Tor Hidden Service Setup

First, let's install `tor` via ports:

```
# cd /usr/ports/net/tor && make && make install
```

Now, edit `/etc/tor/torrc` to configure it:

```
# vi /etc/tor/torrc
```

Uncomment the lines for Hidden Service and save/exit the file:

```
HiddenServiceDir /var/tor/hidden_service/
HiddenServicePort 80 127.0.0.1:80
```

Now enable and start `tor` using `rcctl`:

```
# rcctl enable tor
# rcctl start tor
```

You can check the syslog to make sure it started:

```
# tail /var/log/messages

Apr 29 18:44:22 openbsd Tor[39811]: Tor 0.3.2.10 (git-31cc63deb69db819) running on OpenBSD with Libevent 2.0.22-stable, OpenSSL LibreSSL 2.7.2, Zlib 1.2.3, Liblzma N/A, and Libzstd N/A.
Apr 29 18:44:22 openbsd Tor[39811]: Tor can't help you if you use it wrong! Learn how to be safe at https://www.torproject.org/download/download#warning
Apr 29 18:44:22 openbsd Tor[39811]: Read configuration file "/etc/tor/torrc".
Apr 29 18:44:22 openbsd Tor[39811]: Scheduler type KISTLite has been enabled.
Apr 29 18:44:22 openbsd Tor[39811]: Opening Socks listener on 127.0.0.1:9050
Apr 29 18:44:23 openbsd Tor[39811]: Parsing GEOIP IPv4 file /usr/local/share/tor/geoip.
Apr 29 18:44:24 openbsd Tor[39811]: Parsing GEOIP IPv6 file /usr/local/share/tor/geoip6.
Apr 29 18:44:28 openbsd Tor[39811]: Bootstrapped 0%: Starting
Apr 29 18:44:29 openbsd Tor[39811]: Starting with guard context "default"
Apr 29 18:44:29 openbsd Tor[39811]: Bootstrapped 5%: Connecting to directory server
Apr 29 18:44:29 openbsd Tor[39811]: Bootstrapped 10%: Finishing handshake with directory server
Apr 29 18:44:29 openbsd Tor[39811]: Bootstrapped 15%: Establishing an encrypted directory connection
Apr 29 18:44:29 openbsd Tor[39811]: Bootstrapped 20%: Asking for networkstatus consensus
Apr 29 18:44:29 openbsd Tor[39811]: Bootstrapped 25%: Loading networkstatus consensus
Apr 29 18:44:35 openbsd Tor[39811]: I learned some more directory information, but not enough to build a circuit: We have no usable consensus.
Apr 29 18:44:35 openbsd Tor[39811]: Bootstrapped 40%: Loading authority key certs
Apr 29 18:44:41 openbsd Tor[39811]: Bootstrapped 45%: Asking for relay descriptors
Apr 29 18:44:41 openbsd Tor[39811]: I learned some more directory information, but not enough to build a circuit: We need more microdescriptors: we have 0/6388, and can only build 0% of likely paths. (We have 0% of guards bw, 0% of midp$
Apr 29 18:44:42 openbsd Tor[39811]: I learned some more directory information, but not enough to build a circuit: We need more microdescriptors: we have 0/6388, and can only build 0% of likely paths. (We have 0% of guards bw, 0% of midp$
Apr 29 18:44:42 openbsd Tor[39811]: Bootstrapped 50%: Loading relay descriptors
Apr 29 18:44:46 openbsd Tor[39811]: Bootstrapped 56%: Loading relay descriptors
Apr 29 18:44:47 openbsd Tor[39811]: Bootstrapped 64%: Loading relay descriptors
Apr 29 18:44:47 openbsd Tor[39811]: Bootstrapped 70%: Loading relay descriptors
Apr 29 18:44:48 openbsd Tor[39811]: Bootstrapped 76%: Loading relay descriptors
Apr 29 18:44:48 openbsd Tor[39811]: Bootstrapped 80%: Connecting to the Tor network
Apr 29 18:44:48 openbsd Tor[39811]: Bootstrapped 90%: Establishing a Tor circuit
Apr 29 18:44:49 openbsd Tor[39811]: Tor has successfully opened a circuit. Looks like client functionality is working.
Apr 29 18:44:49 openbsd Tor[39811]: Bootstrapped 100%: Done
Apr 29 19:09:41 openbsd Tor[39811]: Interrupt: exiting cleanly.
Apr 29 19:12:34 openbsd Tor[66561]: Tor 0.3.2.10 (git-31cc63deb69db819) running on OpenBSD with Libevent 2.0.22-stable, OpenSSL LibreSSL 2.7.2, Zlib 1.2.3, Liblzma N/A, and Libzstd N/A.
Apr 29 19:12:34 openbsd Tor[66561]: Tor can't help you if you use it wrong! Learn how to be safe at https://www.torproject.org/download/download#warning
Apr 29 19:12:34 openbsd Tor[66561]: Read configuration file "/etc/tor/torrc".
Apr 29 19:12:34 openbsd Tor[66561]: Scheduler type KISTLite has been enabled.
Apr 29 19:12:34 openbsd Tor[66561]: Opening Socks listener on 127.0.0.1:9050
Apr 29 19:12:36 openbsd Tor[66561]: Parsing GEOIP IPv4 file /usr/local/share/tor/geoip.
Apr 29 19:12:37 openbsd Tor[66561]: Parsing GEOIP IPv6 file /usr/local/share/tor/geoip6.
Apr 29 19:12:44 openbsd Tor[66561]: Bootstrapped 0%: Starting
Apr 29 19:12:49 openbsd Tor[66561]: Starting with guard context "default"
Apr 29 19:12:49 openbsd Tor[66561]: Bootstrapped 80%: Connecting to the Tor network
Apr 29 19:12:51 openbsd Tor[66561]: Bootstrapped 85%: Finishing handshake with first hop
Apr 29 19:12:51 openbsd Tor[66561]: Bootstrapped 90%: Establishing a Tor circuit
Apr 29 19:12:52 openbsd Tor[66561]: Tor has successfully opened a circuit. Looks like client functionality is working.
Apr 29 19:12:52 openbsd Tor[66561]: Bootstrapped 100%: Done
```

Everything looks good, so let's retrieve our hidden service onion name so we can configure the httpd:

```
# cat /var/tor/hidden_service/hostname
4hf84nsot94ba75bg7.onion
```

We have the name, so let's create a root directory for it:

```
# mkdir /var/www/htdocs/4hf84nsot94ba75bg7.onion
```

Excellent, now we will edit `/etc/httpd.conf`:

```
# vi /etc/httpd.conf
```

Paste the following server block to use with your new hidden service, modifying it with your onion name and root folder:

```
server "4hf84nsot94ba75bg7.onion" {
  listen on * port 80
  root "/htdocs/4hf84nsot94ba75bg7.onion"
}
```

Place your site files within `/var/www/htdocs/4hf84nsot94ba75bg7.onion` to populate your site root. For testing, we can make an `index.html` file:

```
# vi /var/www/htdocs/4hf84nsot94ba75bg7.onion/index.html
```

Paste the following and save/exit: 

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

Now we can restart `tor` with `rcctl`:

```
# rcctl restart tor
```

To test, load your onion name in the Tor browser, or from another machine, try to curl with torsocks:

```
$ torsocks curl http://4hf84nsot94ba75bg7.onion
<html>
	<body>
		Hello World!
	</body>
</html>
```

## Sources
* https://www.romanzolotarev.com/openbsd/webserver.html
* https://www.torproject.org/download/download-unix.html.en
* https://www.sccs.swarthmore.edu/users/16/mmcconv1/openbsd-tor.html