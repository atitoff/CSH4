# Micropython

<details><summary>ESP32 + LAN8720 ethernet</summary>

[link](https://github.com/emard/esp32lan8720)

```python
import network
from machine import Pin
lan = network.LAN(mdc=Pin(16), mdio=Pin(17), power=None, id=None, phy_addr=1, phy_type=network.PHY_LAN8720)
lan.active(True)
# by default (no parameters), ifconfig() will request IP from DHCP
lan.ifconfig()
# set fixed IP (address, netmask, gateway, dns)
# lan.ifconfig(('192.168.0.190', '255.255.255.0', '192.168.0.1', '192.168.0.1'))
```


</details>