# Dial-up ISP

One goal I have is to create a Dial-up based ISP. I have a landline, and I also have a VoIP line, one of which should be able to be used directly or in conjunction with a PBX. I have read that multiple VoIP links carrying data can lead to a lot of broken connections, but maybe I could keep a local dial-in server at home.

It looks like you can do this with a Raspberry Pi running `mgetty` and `PPP` with the help of a USB Softmodem adapter (Trendnet makes [a compatible one](https://www.amazon.com/TRENDnet-Data-Modem-TFM-560U-Blue/dp/B00008AWL0)). I don't know if this only really provides remote console access, or if it can just be used through a dial-up wizard and provide the client with 'net access.

You *should* have no issue doing this in theory. Dial-up ISPs operated for a long time and I'm assuming some had Linux.

Here are some useful links:
* Dial UP and PPP server in modern Linux - https://hackaday.io/project/20353-the-retroserver-networking-for-old-computers/log/54966-dial-up-and-ppp-server-in-modern-linux
* How To Set Up Linux As A Dial-In Server  - https://www.howtoforge.com/linux_dialin_server
* TELECOM TIME MACHINE - http://www.instructables.com/id/Telecom-Time-Machine/
* Guest Wifi Access point without access to parent network - https://superuser.com/questions/1310242/guest-wifi-access-point-without-access-to-parent-network
* Dial up server - https://dogemicrosystems.ca/wiki/Dial_up_server
* iptables block 1 ip, nat - https://serverfault.com/questions/290955/iptables-block-1-ip-nat
* How to provide a “guest LAN” on one ethernet device - https://unix.stackexchange.com/questions/46104/how-to-provide-a-guest-lan-on-one-ethernet-device
* Raspberry Pi WireGuard VPN gateway - https://mgnk.it/2019/03/raspberry-pi-as-a-vpn-gateway-using-wireguard/
* Dialup In The Age Of Broadband - https://gekk.info/articles/ata-dialup.html

Other stuff:
* Retro.link - http://retro.link/
