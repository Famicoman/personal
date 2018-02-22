# Dial-up ISP

One goal I have is to create a Dial-up based ISP. I have a landline, and I also have a VoIP line, one of which should be able to be used directly or in conjunction with a PBX. I have read that multiple VoIP links carrying data can lead to a lot of broken connections, but maybe I could keep a local dial-in server at home.

It looks like you can do this with a Raspberry Pi running `mgetty` and `PPP` with the help of a USB Softmodem adapter (Trendnet makes [a compatible one](https://www.amazon.com/TRENDnet-Data-Modem-TFM-560U-Blue/dp/B00008AWL0)). I don't know if this only really provides remote console access, or if it can just be used through a dial-up wizard and provide the client with 'net access.

You *should* have no issue doing this in theory. Dial-up ISPs operated for a long time and I'm assuming some had Linux.

Here are some useful links:
* Dial UP and PPP server in modern Linux - https://hackaday.io/project/20353-the-retroserver-networking-for-old-computers/log/54966-dial-up-and-ppp-server-in-modern-linux
* How To Set Up Linux As A Dial-In Server  - https://www.howtoforge.com/linux_dialin_server
* TELECOM TIME MACHINE - http://www.instructables.com/id/Telecom-Time-Machine/

Also fun, some people are making software that allows you to connect the dial-up adapter on the Sega Dreamcast to a computer acting as something of an Ethernet Bridge. Now you can play all of your online Dreamcast games without needing to shell out for that pricey RJ-45 network adapter.
* DreamPi - http://blog.kazade.co.uk/p/dreampi.html
* You Can Still Use Dial-Up To Surf The Internet With A Dreamcast - http://www.thedreamcastjunkyard.co.uk/2017/03/you-can-still-use-dial-up-to-surf.html
* PC-DC Server Setup (Win98) - http://dreamcast.onlineconsoles.com/phpBB2/guides_pcdcwin98.php
