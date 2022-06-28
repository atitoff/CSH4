#### Шлюз на Perenio

[Ставим OpenWRT на шлюз Perenio PEACG01](https://github.com/DivanX10/Openwrt-scripts-for-gateway-zhwg11lm/wiki/%D0%A1%D1%82%D0%B0%D0%B2%D0%B8%D0%BC-OpenWRT-%D0%BD%D0%B0-%D1%88%D0%BB%D1%8E%D0%B7-Perenio-PEACG01) 

## Mosquitto broker

If you don't have a MQTT broker yet; in Home Assistant go to Settings → Add-ons → Add-on store and install the Mosquitto broker addon.

Go back to the Add-on store, click ⋮ → Repositories, fill in
https://github.com/zigbee2mqtt/hassio-zigbee2mqtt and click Add → Close.

![image](https://user-images.githubusercontent.com/13304485/176131678-ee979698-b83c-4fdb-9568-1a95301e583a.png)

![image](https://user-images.githubusercontent.com/13304485/176135448-3c615c75-3151-48ab-a325-9bf0208731e4.png)

## Zigbee2MQTT

The repository includes two add-ons:
Zigbee2MQTT is the stable release that tracks the released versions of Zigbee2MQTT. (recommended for most users)
Zigbee2MQTT Edge tracks the dev branch of Zigbee2MQTT such that you can install the edge version if there are features or fixes in the Zigbee2MQTT dev branch that are not yet released.
Click on the addon and press Install and wait till the addon is installed.

Click on Configuration
If you are not using the Mosquitto broker addon fill in your MQTT details (leave empty when using the Mosquitto broker addon). Format can be found here, but skip the initial mqtt: indent. e.g.:
```
server: mqtt://localhost:1883
user: mqtt
password: mqtt
```
serial:
```
port: tcp://IP шлюза:5000
adapter: ezsp
```
