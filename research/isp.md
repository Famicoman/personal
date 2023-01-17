# ISP

## Dial-up ISP

One goal I have is to create a Dial-up based ISP. I have a landline, and I also have a VoIP line, one of which should be able to be used directly or in conjunction with a PBX. I have read that multiple VoIP links carrying data can lead to a lot of broken connections, but maybe I could keep a local dial-in server at home.

It looks like you can do this with a Raspberry Pi running `mgetty` and `PPP` with the help of a USB Softmodem adapter (Trendnet makes [a compatible one](https://www.amazon.com/TRENDnet-Data-Modem-TFM-560U-Blue/dp/B00008AWL0)). I don't know if this only really provides remote console access, or if it can just be used through a dial-up wizard and provide the client with 'net access.

You *should* have no issue doing this in theory. Dial-up ISPs operated for a long time and I'm assuming some had Linux.

Here are some useful links:
* RPi - Dial up to Ethernet bridge? - https://www.element14.com/community/thread/56832/l/rpi-dial-up-to-ethernet-bridge?displayFullThread=true
* TRENDnet 56K USB Data/Fax/TAM Modem TFM-560U (Blue) - https://www.amazon.com/TRENDnet-Data-Modem-TFM-560U-Blue/dp/B00008AWL0
* 56k USB Modem for Raspberry Pi - https://old.reddit.com/r/raspberry_pi/comments/4d1z17/56k_usb_modem_for_raspberry_pi/
* Dial UP and PPP server in modern Linux - https://hackaday.io/project/20353-the-retroserver-networking-for-old-computers/log/54966-dial-up-and-ppp-server-in-modern-linux
* How To Set Up Linux As A Dial-In Server  - https://www.howtoforge.com/linux_dialin_server
* TELECOM TIME MACHINE - http://www.instructables.com/id/Telecom-Time-Machine/
* Guest Wifi Access point without access to parent network - https://superuser.com/questions/1310242/guest-wifi-access-point-without-access-to-parent-network
* Dial up server - https://dogemicrosystems.ca/wiki/Dial_up_server
* iptables block 1 ip, nat - https://serverfault.com/questions/290955/iptables-block-1-ip-nat
* How to provide a “guest LAN” on one ethernet device - https://unix.stackexchange.com/questions/46104/how-to-provide-a-guest-lan-on-one-ethernet-device
* Raspberry Pi WireGuard VPN gateway - https://mgnk.it/2019/03/raspberry-pi-as-a-vpn-gateway-using-wireguard/
* Dialup In The Age Of Broadband - https://gekk.info/articles/ata-dialup.html
* How to Setup a Linux Dial-In Server -  https://support.blue.net.au/support/howto-set-up-up-a-linux-dial-in-server/
* Create your own 56K Dialup ISP -  https://shadowram.co.uk/dokuwiki/dialup56k
* Replace login prompt with interactive bash script on serial port linux - https://stackoverflow.com/questions/28035559/replace-login-prompt-with-interactive-bash-script-on-serial-port-linux
* https://unix.stackexchange.com/questions/552576/allow-passwordless-root-login-on-the-serial-console
* Allow passwordless root login on the serial console - https://superuser.com/questions/1392778/how-can-i-spawn-my-own-program-in-a-linux-tty-session-instead-of-the-shell
* mgetty in systemd for modem dial-in server  - https://snarkybrill.blogspot.com/2015/08/mgetty-in-systemd-for-modem-dial-in.html?m=1
* make mystic bbs answer to a modem - http://web.synchro.net/?page=001-forum.ssjs&sub=mystic&thread=5855
* Dial-up vintage BBS access with agetty and a modem - https://unix.stackexchange.com/questions/574149/dial-up-vintage-bbs-access-with-agetty-and-a-modem
* Remote into Ubuntu 14.0.4 that has a USB 56k Modem - https://community.spiceworks.com/topic/1564500-remote-into-ubuntu-14-0-4-that-has-a-usb-56k-modem
* Modem: agetty / mgetty question and terminal dial in. - https://www.reddit.com/r/linuxquestions/comments/eblfng/modem_agetty_mgetty_question_and_terminal_dial_in/?utm_source=amp&utm_medium=&utm_content=comments_view_all
* Getting a dial-up modem working with VoIP - https://area-51.blog/2021/01/16/getting-a-dial-up-modem-working-with-voip/


Other stuff:
* Retro.link - http://retro.link/
* Installing and Configuring Asterisk 18 (with Softmodem) on Ubuntu 20  - https://web.archive.org/web/20211129211259/https://glasstty.com/?page_id=1556
* Automated Computer Time Service - https://www.nist.gov/pml/time-and-frequency-division/time-distribution/automated-computer-time-service-acts

## ISDN

* ISDN: The Untravelled Path of Mobile Computing - https://blog.gatunka.com/2015/06/30/isdn-the-untraveled-path-of-mobile-computing/
* 56K upgrade to the in-home ISP (/u/retrocet) - https://www.reddit.com/r/retrobattlestations/comments/t5m6od/56k_upgrade_to_the_inhome_isp/
* The Home Dialup ISP: Final Edition (now with V.92!) (/u/retrocet) - https://www.reddit.com/r/homelab/comments/vos3w3/the_home_dialup_isp_final_edition_now_with_v92/

## General

* BBSs and early Internet access in the 1990ies  - https://media.ccc.de/v/34c3-9034-bbss_and_early_internet_access_in_the_1990ies