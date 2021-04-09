# WT32-ETH01

Модуль на ESP32 с ethernet LAN8720A (datasheet [pdf](WT32-ETH01_datasheet_V1.1-%20en.pdf))

Может работать с [Micropython](../micropython/readme.md)

![](WT32-ETH01.1.png)

Потребление 80 мА (0,27 Вт), потребление пиковое 500 мА (1,65 Вт).  
PoE не поддерживается, поэтому запитывать придется через дополнительную пару.

![](poe.svg)


## Оживляем

качаем micropython
https://micropython.org/resources/firmware/esp32-idf3-20210202-v1.14.bin

```
pip install esptool
esptool.py --chip esp32 --port COM3 --baud 115200 write_flash -z 0x1000 esp32-idf3-20210202-v1.14.bin
```

Далее ставим

https://thonny.org/

![](thonny_serial.png)

boot.py
```python
# This file is executed on every boot (including wake-boot from deepsleep)
#import esp
#esp.osdebug(None)
import webrepl
import machine
import network

lan = network.LAN(mdc = machine.Pin(23), mdio = machine.Pin(18), power= machine.Pin(16), phy_type = network.PHY_LAN8720, phy_addr=1, clock_mode=network.ETH_CLOCK_GPIO0_IN)
lan.active(True)
lan.ifconfig(('192.168.1.34', '255.255.255.0', '192.168.1.1', '192.168.1.1'))
#               ip                  mask        gateway         dns
webrepl.start()
```

создаем main.py
```python
import machine
import uasyncio as asyncio


pin17 = machine.Pin(17, machine.Pin.OUT)
pin17.value(1)

async def main():
    for i in range(1000):
        await asyncio.sleep_ms(1000)
        print(i)
        if (i % 2) == 0:
            pin17.value(0)
        else:
            pin17.value(1)
        
asyncio.run(main())
```

инициализируем webrepl
```python
import webrepl_setup
```

теперь можно работать через сеть, хотя через COM работает лучше.

![](thonny_webrepl.png)
