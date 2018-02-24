# Amazon Dash Button Hacks

* How I Hacked Amazon's $5 WiFi Button to track Baby Data - https://medium.com/@edwardbenson/how-i-hacked-amazon-s-5-wifi-button-to-track-baby-data-794214b0bdd8#.89bfyzh1w
* Help with python and scapy - Amazon button on Pi - https://www.reddit.com/r/homeautomation/comments/3gy2u7/help_with_python_and_scapy_amazon_button_on_pi/

```from scapy.all import *
def arp_display(pkt):
  if pkt.haslayer(ARP):
    if pkt[ARP].op == 1: #who-has (request)
      if pkt[ARP].psrc == '0.0.0.0': # ARP Probe
        if pkt[ARP].hwsrc == '10:AE:60:9E:C7:A0': # Huggies
          print "Pushed Huggies"

print sniff(prn=arp_display, filter="arp", store=0, count=10)```