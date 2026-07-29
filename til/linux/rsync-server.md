# rsync Server Setup

We want to make a directory shared publicly via `rsync`.

## Install rsync

```
sudo apt update
sudo apt install rsync -y
```

## Create the rsync server config

```
cat /etc/rsyncd.conf

# Global settings
uid = nobody
gid = nogroup
use chroot = yes
max connections = 10
pid file = /var/run/rsyncd.pid
lock file = /var/run/rsync.lock
log file = /var/log/rsyncd.log

[static.philtel.org]
    path = /var/www/static.philtel.org/public
    comment = Public mirror
    read only = yes
    list = yes
	# Optional exclude
	# exclude = /subdirectory/under/path/
```

## Start the service

```
sudo systemctl enable --now rsync
```

## Open 873 TCP

```
sudo iptables -A INPUT -p tcp --dport 873 -j ACCEPT
sudo ip6tables -A INPUT -p tcp --dport 873 -j ACCEPT
```

## Test from another machine

```
sudo apt update
sudo apt install rsync -y
rsync -a --info=progress2 --partial-dir=.rsync-partial rsync://static.philtel.org/static.philtel.org /var/www/html/oddwa.re/public/static.philtel.org
```