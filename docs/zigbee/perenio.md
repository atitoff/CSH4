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
server: mqtt://192.168.1.46:1883
user: mqtt
password: mqtt
```
serial:
```
port: tcp://192.168.1.45:5000
adapter: ezsp
```

Запускаем аддон zigbee2mqtt и заглядываем в журнал. Там должно быть как ниже, где не будет никаких ошибок и должна открыться веб-страница zigbee2mqtt. Если есть ошибки, значит анализируем проблему, возможно неверно указали IP адрес шлюза или порт? или неправильно настроили доступ к MQTT или служба ser2net кем-то занята. Ser2net не может одновременно работать как с zigbee2mqtt и с ZHA. Если запущена интеграция ZHA и она смотрит на ser2net, значит интеграцию ZHA нужно деактивировать, тогда вы сможете запустить аддон zigbee2mqtt
```
[s6-init] making user provided files available at /var/run/s6/etc...exited 0.
[s6-init] ensuring user provided files have correct perms...exited 0.
[fix-attrs.d] applying ownership & permissions fixes...
[fix-attrs.d] done.
[cont-init.d] executing container initialization scripts...
[cont-init.d] socat.sh: executing... 
[18:57:10] INFO: Socat not enabled, marking service as down
[cont-init.d] socat.sh: exited 0.
[cont-init.d] zigbee2mqtt.sh: executing... 
[18:57:10] INFO: MQTT available, fetching server detail ...
[18:57:10] INFO: Previous config file found, checking backup
[18:57:10] INFO: Creating backup config in '/config/zigbee2mqtt/.configuration.yaml.bk'
[18:57:10] INFO: Adjusting Zigbee2mqtt core yaml config with add-on quirks ...
[cont-init.d] zigbee2mqtt.sh: exited 0.
[cont-init.d] done.
[services.d] starting services
[services.d] done.
[18:57:11] INFO: Handing over control to Zigbee2mqtt Core ...
> zigbee2mqtt@1.23.0 start
> node index.js
```
