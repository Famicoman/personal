# Gopher Server Setup

First, let's install `gopher` (the client) via ports:

```
# cd /usr/ports/net/gopher && make && make install
# make clean && make clean-depends
```

Now, will install a gopher daemon. I chose to run `pygopherd`, which relies on python. I previously tried `motsognir` but it doesn't display gophermaps properly and appears to be unmaintained:

```
# cd /usr/ports/net/pygopherd && make && make install
# make clean && make clean-depends
```

The config file is easy to access but has very sane defaults, so it probably doesn't need to be modified:

```
# vi /usr/local/etc/pygopherd/pygopherd.conf
```

When running `pygopherd`, it will drop permissions to a non-root user. Let's set up a `gopher` user:

```
# pw useradd gopher -d /nonexistent
```

Now, we can make an `rc.d` file to run `pygopherd` as a service:

```
# vi /usr/local/etc/rc.d/pygopherd
```

Paste the following and save it:

```
#!/bin/sh
#
# pygopherd.sh for rc.d usage
# $Id$

# PROVIDE: pygopherd
# REQUIRE: DAEMON
# BEFORE: LOGIN
# KEYWORD: shutdown
#
# Add these lines to /etc/rc.conf.local or /etc/rc.conf
# to enable this service:
#
# pygopherd_enable (bool):     Set to NO by default.
#                              Set it to YES to enable pygopherd.

. /etc/rc.subr

name=pygopherd
rcvar=pygopherd_enable

load_rc_config $name

: ${pygopherd_enable:="NO"}

command=/usr/local/bin/${name}
command_interpreter=/usr/local/bin/python2.7

command_args=""

run_rc_command "$1"
```

Next, create the default gopher directory:

```
# mkdir /var/gopher && cd /var/gopher
```

Then, create a sample text file, and a `gophermap` file:

```
# echo "this is a test" >> file.txt
# vi gophermap
```

Paste the following for a simple gophermap and save the file:

```
Welcome to my Gopherspace!

My name is Mike and this is a simple gopherhole.

This gopherhole runs on FreeBSD 11.

This is a test of a file link:

0Just A Test    file.txt

```

Now we can enable the service:

```
#sysrc pygopherd_enable=YES
```

Finally, start the service:

```
service pygopherd start
```

Visit the gopher site with:

```
gopher 127.0.0.1
```

## Sources
* https://github.com/sgolovine/roll-your-gopher/blob/master/README.md
* https://github.com/prologic/gophernicus/blob/master/README.Gophermap
* https://github.com/jgoerzen/pygopherd/blob/master/doc/standards/gophermap.txt
* https://unix.stackexchange.com/questions/398748/what-is-the-freebsd-equivalent-of-linux-update-rc-d