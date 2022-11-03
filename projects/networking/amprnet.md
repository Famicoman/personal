apt install build-essential
wget http://www.yo2loj.ro/hamprojects/ampr-ripd-2.4.tgz
tar -xzf ampr-ripd*
cd ampr-ripd*
make install

modprobe ipip
ip addr add 44.56.66.65/32 dev tunl0
ip link set dev tunl0 up
ip link set mtu 1480 tunl0
./ampr-ripd -d -i tunl0


## DHCPD

```
$ su -
# apt-get install isc-dhcp-server
```

```
# AMPRNet interface
auto enp2s0
iface enp2s0 inet static
        address 44.56.66.64
        netmask 255.255.255.248
```

```
# ifdown enp2s0
# ifup enp2s0
```

```
# nano /etc/dhcp/dhcpd.conf
```

```
authoritative;
subnet 44.56.66.64 netmask 255.255.255.248 {
  range 44.56.66.66 44.56.66.70;
  option routers 44.56.66.65;
  option domain-name-servers 8.8.8.8, 8.8.4.4;
}
```

```
# nano /etc/default/isc-dhcp-server
```

```
INTERFACESv4="enp2s0"
#INTERFACESv6=""
```

```
# systemctl stop isc-dhcp-server
# rm /var/run/dhcpd.pid
# systemctl start isc-dhcp-server
```

