# Micropython

<details><summary>ESP32 + LAN8720 ethernet</summary>


```python
import machine
import network
lan = network.LAN(mdc = machine.Pin(23), mdio = machine.Pin(18), power= machine.Pin(16), phy_type = network.PHY_LAN8720, phy_addr=1, clock_mode=network.ETH_CLOCK_GPIO0_IN)
lan.active(True)
lan.config(dhcp_hostname="module1")
# set fixed IP (address, netmask, gateway, dns)
# lan.ifconfig(('192.168.0.190', '255.255.255.0', '192.168.0.1', '192.168.0.1'))
```


</details>


<details><summary>MicroPython Asynchronous MQTT</summary>

[github](https://github.com/peterhinch/micropython-mqtt/tree/master/mqtt_as)


```python
from mqtt_as import MQTTClient
from config import config
import uasyncio as asyncio

SERVER = '192.168.0.10'  # Change to suit e.g. 'iot.eclipse.org'


def callback(topic, msg, retained):
    print((topic, msg, retained))


async def conn_han(client):
    await client.subscribe('foo_topic', 1)


async def main(client):
    await client.connect()
    n = 0
    while True:
        await asyncio.sleep(5)
        print('publish', n)
        # If WiFi is down the following will pause for the duration.
        await client.publish('result', '{}'.format(n), qos=1)
        n += 1


config['subs_cb'] = callback
config['connect_coro'] = conn_han
config['server'] = SERVER

MQTTClient.DEBUG = True  # Optional: print diagnostic messages
client = MQTTClient(config)
try:
    asyncio.run(main(client))
finally:
    client.close()  # Prevent LmacRxBlk:1 errors
```

</details>


<details><summary>Send manchester code</summary>

```python

```

</details>