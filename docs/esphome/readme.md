# ESPHome

## Hardware

[Список процессоров и модулей ESP32](https://www.espressif.com/en/products/socs/)

### ESP-32S

<details><summary>ESP-32S</summary>

Самый недорогой модуль, несколько устаревший, но вполне работоспособный.

![esp-32s.png](esp-32s.png)

[ESP32.pdf](ESP32.pdf)

</details>

## Сегмент

![segment.svg](segment.svg)


<details><summary>Шаблон кода для модуля с ethernet может быть таким:</summary>

```yaml
substitutions:
  devicename: wt32-0001

esphome:
  name: $devicename
  comment: Living room ESP32 controller
  area: Living Room

esp32:
  board: esp-wrover-kit
  framework:
    type: arduino
    version: latest


ethernet:
  type: LAN8720
  mdc_pin: GPIO23
  mdio_pin: GPIO18
  clk_mode: GPIO0_IN
  phy_addr: 1
  power_pin: GPIO16


# Enable logging
logger:

# Enable Home Assistant API
api:
  encryption:
    key: "TOLsE2i26869JbEJI0r3toI5frqJbreLwvEyZ6bdda4="

ota:
  password: "ase2e12qq"
```

</details>



<details><summary>Работаем с MQTT</summary>

```yaml
mqtt:
  id: mqtt_client
  broker: 192.168.1.194
  username: mqtt
  password: bh0020
  on_connect:
    then:
      - delay: 2s
      - lambda: |-
          ESP_LOGD("mqtt", "Connected to MQTT $devicename");
          id(mqtt_client).publish("$devicename/the/topic", "The Payload");
```

</details>



<details><summary>WiFi по умолчанию отключен</summary>

```yaml
wifi:
  enable_on_boot: false

api:
  reboot_timeout: 0s

on_...:
  then:
    - wifi.disable:

on_...:
  then:
    - wifi.enable:
```

</details>



<details><summary>Субмодули общаются по CAN</summary>

```yaml
substitutions:
  module_id: 1  # номер модуля на CAN шине от 0 до 15

esphome:
  name: module
  name_add_mac_suffix: true

wifi:
  enable_on_boot: false

api:
  reboot_timeout: 0s

on_...:
  then:
    - wifi.disable:

on_...:
  then:
    - wifi.enable:

canbus:
  - platform: ...
    can_id: $module_id
    bit_rate: 25KBPS
    on_frame:
    - can_id: 16
      use_extended_id: false
      then:
      - lambda: |-
```

</details>