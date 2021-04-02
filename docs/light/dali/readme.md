# DALI

в основном взято [отсюда](01465a.pdf)

* интерфейс на базе [ESP32ETH](esp32eth/readme.md)

## Передача сигнала

![](dali_transmission.png)

### Frame timing

![](frame_timing.svg)

### Принцип декодирования

![](decoding.svg)


## Команды DALI

[см.](command.md)

## Команды DALI MQTT

`dali/ha/SET_LEVEL/32` **Установить яркость светильника** 32 | payload = 0..254
`dali/ha/SET_LEVEL_GRP/12` **Установить яркость группы** 12 | payload = 0..254

payload

| byte |  |
| ---- | ----|
| 0 | level 0..255 |

## Схемы

### Схема с опторазвязкой

![](opto_schematic.png)

Q2 - 600mA, 40V, hfe 100..300  
U1, U2 - TLP183