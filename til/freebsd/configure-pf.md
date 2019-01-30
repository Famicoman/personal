# Configure PF

Let's get PF running as a basic firewall.

First, let's enable `pf` in `rc.conf`:

```
# vi /etc/rc.conf
```

Add the following to the bottom:

```
pf_enable="YES"
pf_rules="/etc/pf.conf"
pflog_enable="YES"
pflog_logfile="/var/log/pflog"
```

Now we need to define our rules, so let's create `pf.conf`:

```
# vi /etc/pf.conf
```

Past the following basic config:

```
# INTERFACES check if ext_if matches the network card name
# (ifconfig tells it)

loc_if="lo0"	# Our loopback
net_if="re0"	# Our physical adapter
ygg_if="tap0"	# Our TAP adapter, this one if for yggdrasil

# NORMALIZATION
scrub in all

# BLOCK INCOMING
block in on $ygg_if

# ALLOW INCOMING
pass in on $ygg_if proto icmp6 all
pass in on $loc_if all
pass in on $net_if all

# ALLOW OUTGOING TRAFFIC
pass out on $loc_if all
pass out on $net_if all
pass out on $ygg_if all
```

Now we can check the config to make sure the rules are valid:

```
# pfctl -n -v -f /etc/pf.conf
```

If all goes well, we can start it up:

```
# service start pf
```